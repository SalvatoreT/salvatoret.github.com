---
layout: post
title: How I added the Kotlin Interactive Shell to Homebrew (and you can too)
published: true
category: open-source
image: /assets/article_images/2021-05-16-adding-kotlin-interactive-shell-to-homebrew/Homebrew-Kotlin-Tile.svg
image2: /assets/article_images/2021-05-16-adding-kotlin-interactive-shell-to-homebrew/Homebrew-Kotlin-Tools.svg
tags: [homebrew, kotlin, java]
---
I really like `ki`, but I didn't want to run the shell script every time. [Other folks felt the same](https://github.com/Kotlin/kotlin-interactive-shell/issues/58), so I ended up writing [this Homebrew formula](https://github.com/Homebrew/linuxbrew-core/blob/e7d0a0691bb54b93546a1b10fce8a199d1bcecbe/Formula/ki.rb). Here's an abbreviated version of how I did it.

# How does Homebrew work?

Homebrew is a package manager and artifact builder. All of the programs/tools/packages that core Homebrew knows about are located at `brew --repo homebrew/core` repository.

![For me, it's "/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core"](/assets/article_images/2021-05-16-adding-kotlin-interactive-shell-to-homebrew/sublime-homebrew-core-list.jpg)

The repository contains instructions (called formulae) for the Homebrew build servers to make and test the programs. Once the build servers build the formulae, they store the result as "bottles". When you run `brew install <formula>`, you download the bottle along with any other dependency.

# Creating the Ki formula

Getting started is super easy because Homebrew has a command to generate a template formula. In my case, I ran the following by pointing at the released version of `ki`.

{% highlight bash %}
brew create https://github.com/Kotlin/kotlin-interactive-shell/archive/refs/tags/v0.3.3.tar.gz
{% endhighlight %}

... which resulted in (more-or-less) this:

{% highlight ruby %}
class KotlinInteractiveShell < Formula
  desc "Kotlin Language Interactive Shell"
  url "https://github.com/Kotlin/kotlin-interactive-shell/archive/refs/tags/v0.3.3.tar.gz"
  sha256 "46913b17c85711213251948342d0f4d0fec7dc98dd11c1f24eedb0409338e273"
  license "Apache-2.0"

  def install
    # ...
  end

  test do
    # ...
  end
end
{% endhighlight %}

I renamed the generated `kotlin-interactive-shell.rb` file to `ki.rb` and changed the `KotlinInteractiveShell` class name to `Ki` because I wanted the command line tool to be `ki`.

# Build Ki locally (think globally)

The only build dependency is Maven, and the runtime is Java, so those are the only two packages I needed to call out.

{% highlight ruby %}
depends_on "maven" => :build
depends_on "openjdk"
{% endhighlight %}

I then took the build instructions from the `ki` [README](https://github.com/Kotlin/kotlin-interactive-shell/blob/b13fc02d19f170f92525ad17108862abdf6d3416/README.md#build-from-source) and plopped them into the install block. I put the Java artifact into the `libexec` folder to avoid name collisions, which I learned about [from this StackExchange post](https://apple.stackexchange.com/a/277658).

Homebrew has some nice pre-built commands [including one for wiring up JAR files](https://rubydoc.brew.sh/Pathname#write_jar_script-instance_method), so making the command line script is also very little work.

{% highlight ruby %}
def install
  system "mvn", "-DskipTests", "package"
  libexec.install "lib/ki-shell.jar"
  bin.write_jar_script libexec/"ki-shell.jar", "ki"
end
{% endhighlight %}

To test out my script, I made my laptop pretend it was a Homebrew build server, and built the package.

{% highlight bash %}
brew install --build-from-source ki
{% endhighlight %}

I didn't actually write the correct code the first time, so I ran the build command with an additional `--debug` flag that let me try things out in the build environment. I spent most of my time doing this.

# Test it out

The `test` block of the formula is a very basic check to see if the tool runs at all. I tried to not over-think it.

When you run the `ki` shell, and then close it, this is the output.

{% highlight bash %}
$ ki
ki-shell 0.3/1.4.32
type :h for help
[0] :q

Bye!
{% endhighlight %}

For my test, I just wanted to make sure the initial "ki-shell" and final "Bye!" message appeared.

{% highlight ruby %}
test do
  output = pipe_output(bin/"ki", ":q")
  assert_match "ki-shell", output
  assert_match "Bye!", output
end
{% endhighlight %}

I then tested with `brew test ki`. My first draft of the `test` also didn't work, so I used the `--debug` flag here too.

When the test worked, I made sure the automated auditor passed.

{% highlight bash %}
brew audit --strict --online ki
{% endhighlight %}

# Open the pull request

Last, but not least I [opened up a pull request](https://github.com/Homebrew/homebrew-core/pull/74409) against the [Homebrew/homebrew-core](https://github.com/Homebrew/homebrew-core) repo and watched the tests run.

![Green tests are the best tests](/assets/article_images/2021-05-16-adding-kotlin-interactive-shell-to-homebrew/Homebrew-pipeline-tests-passing.jpg)

Once [all of the tests passed](https://github.com/Homebrew/homebrew-core/runs/2487784071), and I got sign-off from the reviewers, the formula was merged, and Homebrew built `ki` [for the various macOS environments](https://github.com/Homebrew/linuxbrew-core/commit/e7d0a0691bb54b93546a1b10fce8a199d1bcecbe).

I ran `brew install ki`, and was very excited to see it work.

# Look around and borrow

Most of everything I did, I figured out by looking at [other formulae](https://github.com/Homebrew/homebrew-core/tree/master/Formula), trial, and error. If you ever decide to write a formula, you might want to do the same.
