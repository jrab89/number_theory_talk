layout: true
class: middle

---

# Number Theory: Why Cryptography Works

???
Presenter notes go here
'P' toggles presenter mode
'C' clones the slideshow in a new tab

---

About me...

---

class: center

# But first...

--


![Larry Wall](Larry_Wall.jpg)


--

# Larry's Three Great Virtues of a Programmer:

???
Before we get into Number Theory, I'd like to talk about Larry Wall a bit. For those of who don't know, Larry Wall is the author of the Perl programming language. But wait! This is a Ruby Meetup, why are we talking about Perl? Well, we're not really talking about Perl, but even if we were I don't think that would necessarily be crazy since Ruby was heavily inspired by Perl. But what I would like to touch on is Larry Wall's three virtues of a great programmer.

---

# 1. Laziness

  _"The quality that makes you go to great effort to reduce overall energy expenditure. It makes you write labor-saving programs that other people will find useful, and document what you wrote so you don't have to answer so many questions about it. Hence, the first great virtue of a programmer."_

---

# 2. Impatence

  _"The anger you feel when the computer is being lazy. This makes you write programs that don't just react to your needs, but actually anticipate them. Or at least pretend to. Hence, the second great virtue of a programmer."_

---

# 3. Hubris

  _"Excessive pride, the sort of thing Zeus zaps you for. Also the quality that makes you write (and maintain) programs that other people won't want to say bad things about. Hence, the third great virtue of a programmer."_

---

# And now for the disclaimer...

--

1. Be lazy, someone else has already done it for you

--

2. Be impatent, review takes a long time

--

3. Have hubris, avoid people saying bad things about your software by not writing it to begin with

???
I think these are some really valuably insights that can lead us to better solve problems, and also solve the better problems. I also think they make for three really good reasons that you probably shouldn't be writing your own cyptographic code, especially when it would be really bad if it didn't exactly work as you had intended.

That being said a great way to learn about Number Theory and Cryptography (or really anything) is do it yourself! And yeah maybe even use it on your blog or your iPhone app your working on that lets people share where with eachother where all the best Pokemons are at! But probably don't use your own cryptosystem if your trying to do things like protect people's medical or financial data.

---

What is a proof?

You might think of a proof from a math class you had, but proofs exist outside mathematics.

So what's a higher level notion of what a proof is?

Across many fields, a proof is a method for ascertaining truth:

* Observation and experimentation
  - What makes physics work
  - If we do an experiment 10 times, and every time it comes out the same way, we've ascertained some truth
  - Who really knows if there is gravity? We observe it, and then that's the truth: there is gravity
    * We see how it behaves under different cicrumstances, then we make generalizations
    * We verify those generalizations through experimentation, then those become laws
* Truth is established by juries and judges
  - Someone has alledgedly done a bad thing, witnesses say they saw this person do that, a jury finds this to be compelling evidence, then a verdict is made
  - Not always 100% effective, but like the other methods of proof, it is a method for ascertaining the truth
  - Marge in chains, Bart Gets Hit By a Car
* Sometimes truth comes from authority
  - Truth can get complicated when you have conflicting truths: someone thinks one thing, someone else thinks another
  - Some places I've worked I had superiors that when they said something that was the truth, and you better be okay with that or "you're fired"
  - Teachers or professors, how you did on assignment or test is up to them
* Inner Conviction
  - Popular in computing
    * Emacs vs Vim
    * Tabs vs spaces
    * Ruby vs Python (that other language with the snake)
    * "My code doesn't have any bugs!"
  - "I don't see why not"
    * Particularly effective, since it tranfers the burden of proof to anyone who disagrees with you
    * Now your view is correct until someone else disproves you
* Mathematic Proof: a verification of a proposition by a chain of logical deductions from a set of axioms
  - Proposition: a statement that is true of false
    * e.g. 2 + 3 = 5
    * ∀n ∈ ℕ, n^2 + n + 41 is a prime number
      - ∀ => "For all"
      - ∈ => "is a member of"
      - ℕ => the natural numbers (non-negative integers)
      - prime number => an integer divisible only by itself and 1
      - predicate => "n^2 + n + 41 is a prime number" in this case, a proposition whose truth depends on some variable(s), n in this case
        * Like a method that returns a boolean in Ruby, e.g.
          ```ruby
          def even?(n)
            n % 2 == 0
          end
          ```
        * This particular predicate can be written as:
          ```ruby
          require 'prime'

          def n_squared_plus_n_plus_41_prime?(n)
            Prime.prime?(n ** 2 + n + 41)
          end
          ```
        * Maybe we can approach this the way physicists do? Lets try a bunch of values for n and see if the results are prime:
          ```
          (1..20).map { |n| n_squared_plus_n_plus_41_prime?(n) }.all?
          # => true
          ```
        * At this point can we say the proposition is true? Lets keep trying:
          ```
          (21..39).map { |n| n_squared_plus_n_plus_41_prime?(n) }.all?
          # => true
          n_squared_plus_n_plus_41_prime?(40)
          # => false
          40 ** 2 + 40 + 41 == 41 * 41
          # => true
          ```
        * Not as rare or contrived an example as you'd guess
        * Many propositions that seem to be true when you check a few cases (or _a lot_ of cases), but which turn out to be false
        * You can’t check a claim about an infinite set by checking a finite set of its elements, no matter how large the finite set!
