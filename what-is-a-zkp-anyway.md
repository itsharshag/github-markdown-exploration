# What the Heck is a Zero-Knowledge Proof, Anyway?

Whenever public blockchains are brought up, two big criticisms follow close behind: “They don’t scale!” goes the first one, and “There’s absolutely no privacy!” goes the second.

Maybe public blockchains offer great censorship resistance, but if they can’t scale and keep transactions private, how will they ever reach the masses?

There’s a lot of truth to these criticisms, and we’ve been searching for solutions for nearly a decade. Plenty of sharp engineers went on to build new blockchains for this reason, cleverly restructuring them so they could scale more elegantly than Bitcoin and Ethereum. But there are no free lunches, as they say. Scalability comes at a cost, and it’s a steep one — the trade-off is decentralization and security.

Until now.

It might sound too good to be true, but a revolutionary technology called “zero-knowledge proofs” seems to have solved both of these problems.

We’ll get into the weeds in a moment, but for now, know that zero-knowledge technology helps us scale blockchains by compressing data while still being able to verify its authenticity. Projects such as [zkSync](https://zksync.io/) and [Loopring](https://loopring.org/#/) are building zk-rollups on Ethereum to do just that.

Zero-knowledge technology also maintains privacy because everyone can verify the authenticity of data, even though they can’t access the underlying data. Projects like [Aztec](https://aztec.network/) are building a privacy layer for Ethereum using zero-knowledge technology.

So, this is exciting stuff!

But understanding how it works is no simple feat. Most people who try to learn about zero-knowledge technology don’t get very far. After all, it’s a complicated topic that requires a lot of math and cryptography knowledge just to begin making sense of it.

That brings us to this article. Without getting bogged down in the complexities of zero-knowledge proofs, we’ll get to the big picture and build an intuition around it through digestible examples. Consider this the first part in a series unraveling zero-knowledge proofs, from overviews to details.

Without further ado, let’s get started!

## What is a Zero-Knowledge Proof?

A zero-knowledge proof is a method that allows one party (Peggy) to prove to another (Victor) that she knows a secret value that fulfills some constraints — without revealing any additional information to Victor, only that she knows this secret value.

In a zero-knowledge protocol, we refer to the secret value as the “_witness_” and the two parties as the “_Prover”_ and “_Verifier”._

1.  **Prover:** The _prover_ (“Peggy”) wants to prove to the _verifier_ (“Victor”) that she knows the _witness_ without revealing the witness.
2.  **Verifier:** The _verifier_ needs to verify that the _prover_ does know the _witness_ without revealing the _witness_ to himself or anyone else.

\[ADD IMAGE OF PEGGY AND VICTOR. PEGGY IS TELLING VICTOR THAT SHE KNOWS THE WITNESS AND VICTOR WANTS PROOF\]

For a zero-knowledge protocol to be valid, it has to satisfy three properties:

1.  **Soundness**: If the proof is valid, it must be accepted by the verifier (ie. a correct proof is always accepted).
2.  **Completeness**: If the proof is invalid, it must be rejected by the verifier (ie. the probability that a verifier accepts an incorrect solution is negligible).
3.  **Zero-Knowledge**: The verifier does not learn any information about the information that the prover claims to know other than the assertion that she knows it.

Let’s look at a few examples demonstrating the concept of proving that you know something while leaking no knowledge of that thing. It sounds contradictory at first, but you’ll begin to see that it is not as strange as it sounds.

## Example 1: Finding Waldo

“Where’s Waldo?” is a game where you have to find the titular Waldo (who looks like the image below) in a sea of characters and shapes that look like him.

\[ADD IMAGE OF WALDO AND IMAGE OF WALDO PUZZLE\]

Let’s assume that Peggy found Waldo and wants to prove to Victor that she knows where Waldo is — without revealing his location in the puzzle.

There are two ways she can do this:

### Solution 1: Cut Out Waldo

Imagine that Peggy cuts out Waldo from the puzzle and shows Victor the Waldo cutout.

\[ADD IMAGE OF WALDO SNIPPET\]

This begs the question. What if she just printed out a picture of Waldo and fooled Victor into thinking she found Waldo? How do we know she cut the snippet from the original puzzle?

To ensure that Peggy didn’t just cut out a picture of Waldo from somewhere, Victor can watermark the back of the puzzle. If Peggy’s cutout consists of the watermark, then Victor can be sure that Peggy did in fact find Waldo in the original puzzle.

\[ADD WALDO SNIPPET WITH WATERMARK IN THE BACK\]

### Solution 2: Show Waldo Through a Hole

Imagine Peggy takes a very large and opaque piece of paper and cuts a small hole in it. She places the hole on top of the puzzle such that Waldo is visible through the hole. This shows that she knows where Waldo is, but Victor won’t be able to figure out Waldo’s location within the puzzle. You could imagine that the piece of paper is much larger than the original puzzle so figuring out the location of Waldo based on the cutout is not possible.

\[ADD IMAGE OF PAPER WITH HOLE + PUZZLE UNDERNEATH\]

### Soundness, Completeness, and Zero-Knowledge

Now, let’s understand how these solutions satisfy the three properties.

**Soundness**

Recall that soundness means that a correct proof must be accepted. In either case, whether Peggy successfully provides a cutout of Waldo from a watermarked puzzle or uses a large opaque paper to display Waldo through a hole, Victor will accept the proof because he knows she can’t cheat.

**Completeness**

Completeness means that an invalid proof won’t be accepted. In solution one, by watermarking the puzzle, we make sure that if Peggy tries to fool Victor with a cutout of Waldo which doesn’t have a watermark, then he knows not to accept it. In solution two, we can ask Peggy to reproduce the original puzzle to make sure she is showing us Waldo from the original puzzle and not from a different one.

**Zero-knowledge**

Zero-knowledge means only the statement that is being proven is revealed. In either solution, Peggy is able to prove to Victor she knows the solution without him knowing where Waldo is (ie. Waldo’s location within the puzzle is never revealed).

## Example 2: Color Blindness

Imagine Peggy has two colored balls — one is red, and the other is blue. Since Victor is colorblind, he might not believe that the balls are different colors. Peggy, who isn’t colorblind, wants to prove to Victor that the balls are different colors, even though she can’t actually reveal the colors.

How can Victor verify Peggy’s claim?

Simple. Peggy takes the two colored balls and hands them to Victor. Victor puts both balls behind his back and then brings one out from behind his back and shows it to Peggy. He then puts the ball behind his back again and then brings one back. He asks her, “Did I switch the ball?”

Since Peggy isn’t colorblind, she can confidently answer Victor’s question.

\[ADD ILLUSTRATION OF VICTOR SHOWING ONE BALL TO PEGGY\]

But she still hasn’t proven much. After all, the odds of being correct are 50%. Peggy could have gotten lucky with her first guess. So, Victor decides to repeat the process dozens of times. If Peggy provides the right answer, he can be sure the balls are different colors.

You’ll notice that, unlike finding Waldo, this example required many repetitions, where Peggy and Victor had to interact back-and-forth until Victor was convinced that Peggy was not colorblind.

\[ADD BACK AND FORTH INTERACTION DIAGRAM SIMILAR TO [THIS](https://medium.com/xord/zero-knowledge-proofs-a-general-understanding-xord-67928f3eea7f)\]

The key point to take away from this example is that the zero knowledge scheme was _probabilistic_. While there isn’t a 100% guarantee that Peggy is not color-blind, if we run the process even just two dozen times, we can be 99.9999999404% certain that Peggy can see colors.

The probability of the incorrect answer is 1/2, so if we repeat the process n times, then the probability of getting it correct n times is 1 - 1/2^(n), where n is the number of repetitions. Real-world ZK proofs work the same way — they offer probabilistic guarantees of soundness and completeness.

### Soundness, Completeness, and Zero-Knowledge

Now, let’s take a look at how the above proof meets our three criteria:

**Soundness**

If Peggy is not colorblind, then by continuously giving the right answer to Victor about whether the balls are switched or not, she can prove to Victor that she can see colors.

**Completeness**

If Peggy’s claim is false and she is colorblind, then the probability of Victor accepting her proof is negligible because Peggy will eventually not be able to tell if the balls were switched or not.

**Zero Knowledge**

Victor has not learned about the actual colors of the balls, despite being able to verify that Peggy can distinguish the colors of the balls.

So, this solution works, but it definitely isn’t efficient or practical. It requires the verifier and prover to be available and interact repeatedly. Even if a verifier was convinced of a prover’s honesty, if another verifier wants to do the same, they have to start the whole interaction from scratch.

To solve this inefficiency, “non-interactive” proofs were invented. We’ll take a look at how these work in the next example.

## Example 3: Hash function

Peggy knows some secret value “w” which, when hashed, results in “x.” Peggy needs to prove to Victor that she knows “w” without actually revealing “w.” Peggy can use a zero-knowledge proof for this.

We can convert the above scenario into a simple program:

The program takes in “x” (the hash of the secret value) and the secret value “w.” It returns true if the SHA-256 hash of “w” equals “x.”

\[CAN WE HAVE A COOL ANIMATION HERE WHERE THE FUNCTION TAKES SOME VALUE OF W AND X AND IT ANIMATES TO RETURN TRUE OR FALSE\]

So, Peggy needs to prove that she knows a value “w” that will result in the program above returning _true_.

### The Basic Elements of Zero-Knowledge Proofs

In order to explain the solution to this problem, we need to understand the basic elements of zero-knowledge proofs — specifically “zk-SNARK” proofs.

zk-SNARK is an acronym that stands for “Zero-Knowledge Succinct Non-Interactive Argument of Knowledge.” Let’s break that down:

- **S = Succinct:** The proofs for even very large programs are small (eg. a few hundred bytes) and can be verified within a few milliseconds.
- **N = Non-interactive:** There is no need for back-and-forth communication between a prover and verifier (eg. such as in the “Color Blindness” example above). Instead, a prover simply hands over a proof to the verifier and the verifier can compute whether the proof is valid or invalid.
- **AR = Argument:** For technical reasons, the proofs are called “arguments” because they are not technically “proofs” in the traditional sense — but they functionally serve the same purpose. The difference between “proof” and “argument” is very technical and out of scope for this post.
- **K = Knowledge:** This refers to the information that the prover knows.

Roughly speaking, a zk-SNARK consists of three algorithms: Generator, Verifier, and Prover. We’ll take a look at each of them now.

#### Generator

The generator algorithm, “G”, generates two keys: the proving key (“pk”) and verification key (“vk”). In order to generate these keys, it takes as inputs a secret parameter (“lambda”) and a program C (such as the one we defined above, which returns true if the hash of “w” matches “x”).

$(pk, vk) = G(lambda, C)$

The proving and verification keys created by the generator are public and used by the prover and verifier, respectively, to generate the proof and verify the proof.

#### Prover

The prover algorithm, “P”, is responsible for generating the zero-knowledge proof. It takes as inputs the proving key (“pk”), the private witness “w,” and a public value “x” to generate the proof.

$proof = P(pk, x, w)$

The witness (“w”) is the secret information that the prover claims she has knowledge of, while the value “x” is a value that is generated based on “w” but is obfuscated such that anyone can access “x” without figuring out “w.”

#### Verifier

The verifier algorithm (“V”) is responsible for taking the proof created by the proving algorithm and asserting true or false, depending on whether the proof is correct or incorrect. It takes as inputs the verification key (“vk”), the public value “x,” and the “proof”.

$V(vk, x, proof) = bool$

#### Putting It All Together

Now, let’s revisit our problem statement. As a quick refresher, Peggy knows some secret value (“w”) which, when hashed, results in “x.” Peggy needs to prove to Victor that she knows “w” without actually revealing “w.”

Let’s see how this would look using a zk-SNARK, step by step.

**Step 1: Generate the Program/Constraints**

This is the program that tells us what knowledge we’re looking for. In our case, we have the constraint that the hash of “w” must equal “x.”

**Step 2: Generate Keys**

This requires us to select the secret parameter “lambda,” which must be done very carefully. If lambda is leaked, then anyone who has access to it can generate fake proofs. This is why zk-SNARKs require what is called a “trusted setup” phase where the keys are generated, but we have to trust that the lambda value was discarded properly and not leaked.

$(pk, vk) = G(C, lambda)$

**Step 3: Generate Proof**

Peggy can now use the proving key, the hash of her secret value, and the secret value to generate the proof:

$proof = P(pk, x, s)$

**Step 4: Verify the Proof**

Victor takes the proof, the hash of the secret value, and verification key and runs it through the verification algorithm to figure out whether Alice’s proof is valid or not.

$V(vk, x, proof) = true$

And there you have it!

But before we wrap up, let’s check back in with our three criteria.

Assuming that we take the G, P, and V algorithms as black boxes, where we agree on the inputs and outputs and trust that the internals work as intended, then we can see how the solution exhibits soundness, completeness, and zero knowledge.

Here’s how:

**Soundness**

The program “C” returns “true” when Peggy’s secret input value (“w”) is the right value. So, Peggy’s proof will be accepted by Victor.

**Completeness**

If the program “C” returns “false,” then the Verifier algorithm will return false and Victor will not accept the invalid proof.

**Zero Knowledge**

Victor is able to verify that Peggy knows “w” without gaining any knowledge of the value “w.”

Of course, the devil is in the details. Understanding how these black boxes work is not trivial, but not impossible either. We will be breaking down different components and aspects of zero knowledge technology in future posts. Stay tuned!

**Reference material:**

[Understanding Zero-knowledge proofs through illustrated examples](https://blog.goodaudience.com/understanding-zero-knowledge-proofs-through-simple-examples-df673f796d99)

[Introduction to zk-SNARKs](https://consensys.net/blog/developers/introduction-to-zk-snarks/)
