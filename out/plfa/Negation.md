---
title     : "Negation: Negation, with intuitionistic and classical logic"
layout    : page
permalink : /Negation/
---

<pre class="Agda">{% raw %}<a id="137" class="Keyword">module</a> <a id="144" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}" class="Module">plfa.Negation</a> <a id="158" class="Keyword">where</a>{% endraw %}</pre>

This chapter introduces negation, and discusses intuitionistic
and classical logic.

## Imports

<pre class="Agda">{% raw %}<a id="286" class="Keyword">open</a> <a id="291" class="Keyword">import</a> <a id="298" href="https://agda.github.io/agda-stdlib/Relation.Binary.PropositionalEquality.html" class="Module">Relation.Binary.PropositionalEquality</a> <a id="336" class="Keyword">using</a> <a id="342" class="Symbol">(</a><a id="343" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Equality.html#83" class="Datatype Operator">_≡_</a><a id="346" class="Symbol">;</a> <a id="348" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Equality.html#140" class="InductiveConstructor">refl</a><a id="352" class="Symbol">)</a>
<a id="354" class="Keyword">open</a> <a id="359" class="Keyword">import</a> <a id="366" href="https://agda.github.io/agda-stdlib/Data.Nat.html" class="Module">Data.Nat</a> <a id="375" class="Keyword">using</a> <a id="381" class="Symbol">(</a><a id="382" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Nat.html#97" class="Datatype">ℕ</a><a id="383" class="Symbol">;</a> <a id="385" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Nat.html#115" class="InductiveConstructor">zero</a><a id="389" class="Symbol">;</a> <a id="391" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Nat.html#128" class="InductiveConstructor">suc</a><a id="394" class="Symbol">)</a>
<a id="396" class="Keyword">open</a> <a id="401" class="Keyword">import</a> <a id="408" href="https://agda.github.io/agda-stdlib/Data.Empty.html" class="Module">Data.Empty</a> <a id="419" class="Keyword">using</a> <a id="425" class="Symbol">(</a><a id="426" href="https://agda.github.io/agda-stdlib/Data.Empty.html#243" class="Datatype">⊥</a><a id="427" class="Symbol">;</a> <a id="429" href="https://agda.github.io/agda-stdlib/Data.Empty.html#360" class="Function">⊥-elim</a><a id="435" class="Symbol">)</a>
<a id="437" class="Keyword">open</a> <a id="442" class="Keyword">import</a> <a id="449" href="https://agda.github.io/agda-stdlib/Data.Sum.html" class="Module">Data.Sum</a> <a id="458" class="Keyword">using</a> <a id="464" class="Symbol">(</a><a id="465" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">_⊎_</a><a id="468" class="Symbol">;</a> <a id="470" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#470" class="InductiveConstructor">inj₁</a><a id="474" class="Symbol">;</a> <a id="476" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#495" class="InductiveConstructor">inj₂</a><a id="480" class="Symbol">)</a>
<a id="482" class="Keyword">open</a> <a id="487" class="Keyword">import</a> <a id="494" href="https://agda.github.io/agda-stdlib/Data.Product.html" class="Module">Data.Product</a> <a id="507" class="Keyword">using</a> <a id="513" class="Symbol">(</a><a id="514" href="https://agda.github.io/agda-stdlib/Data.Product.html#1329" class="Function Operator">_×_</a><a id="517" class="Symbol">;</a> <a id="519" href="https://agda.github.io/agda-stdlib/Data.Product.html#559" class="Field">proj₁</a><a id="524" class="Symbol">;</a> <a id="526" href="https://agda.github.io/agda-stdlib/Data.Product.html#573" class="Field">proj₂</a><a id="531" class="Symbol">)</a> <a id="533" class="Keyword">renaming</a> <a id="542" class="Symbol">(</a><a id="543" href="https://agda.github.io/agda-stdlib/Data.Product.html#543" class="InductiveConstructor Operator">_,_</a> <a id="547" class="Symbol">to</a> <a id="550" href="https://agda.github.io/agda-stdlib/Data.Product.html#543" class="InductiveConstructor Operator">⟨_,_⟩</a><a id="555" class="Symbol">)</a>
<a id="557" class="Keyword">open</a> <a id="562" class="Keyword">import</a> <a id="569" href="https://agda.github.io/agda-stdlib/Function.html" class="Module">Function</a> <a id="578" class="Keyword">using</a> <a id="584" class="Symbol">(</a><a id="585" href="https://agda.github.io/agda-stdlib/Function.html#759" class="Function Operator">_∘_</a><a id="588" class="Symbol">)</a>
<a id="590" class="Keyword">open</a> <a id="595" class="Keyword">import</a> <a id="602" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}" class="Module">plfa.Isomorphism</a> <a id="619" class="Keyword">using</a> <a id="625" class="Symbol">(</a><a id="626" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}#4128" class="Record Operator">_≃_</a><a id="629" class="Symbol">;</a> <a id="631" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}#6826" class="Function">≃-sym</a><a id="636" class="Symbol">;</a> <a id="638" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}#7167" class="Function">≃-trans</a><a id="645" class="Symbol">;</a> <a id="647" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}#9037" class="Record Operator">_≲_</a><a id="650" class="Symbol">)</a>{% endraw %}</pre>


## Negation

Given a proposition `A`, the negation `¬ A` holds if `A` cannot hold.
We formalise this idea by declaring negation to be the same
as implication of false.
<pre class="Agda">{% raw %}<a id="¬_"></a><a id="846" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬_</a> <a id="849" class="Symbol">:</a> <a id="851" class="PrimitiveType">Set</a> <a id="855" class="Symbol">→</a> <a id="857" class="PrimitiveType">Set</a>
<a id="861" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="863" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#863" class="Bound">A</a> <a id="865" class="Symbol">=</a> <a id="867" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#863" class="Bound">A</a> <a id="869" class="Symbol">→</a> <a id="871" href="https://agda.github.io/agda-stdlib/Data.Empty.html#243" class="Datatype">⊥</a>{% endraw %}</pre>
This is a form of _proof by contradiction_: if assuming `A` leads
to the conclusion `⊥` (a contradiction), then we must have `¬ A`.

Evidence that `¬ A` holds is of the form

    λ{ x → N }

where `N` is a term of type `⊥` containing as a free variable `x` of type `A`.
In other words, evidence that `¬ A` holds is a function that converts evidence
that `A` holds into evidence that `⊥` holds.

Given evidence that both `¬ A` and `A` hold, we can conclude that `⊥` holds.
In other words, if both `¬ A` and `A` hold, then we have a contradiction.
<pre class="Agda">{% raw %}<a id="¬-elim"></a><a id="1443" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1443" class="Function">¬-elim</a> <a id="1450" class="Symbol">:</a> <a id="1452" class="Symbol">∀</a> <a id="1454" class="Symbol">{</a><a id="1455" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1455" class="Bound">A</a> <a id="1457" class="Symbol">:</a> <a id="1459" class="PrimitiveType">Set</a><a id="1462" class="Symbol">}</a>
  <a id="1466" class="Symbol">→</a> <a id="1468" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="1470" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1455" class="Bound">A</a>
  <a id="1474" class="Symbol">→</a> <a id="1476" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1455" class="Bound">A</a>
    <a id="1482" class="Comment">---</a>
  <a id="1488" class="Symbol">→</a> <a id="1490" href="https://agda.github.io/agda-stdlib/Data.Empty.html#243" class="Datatype">⊥</a>
<a id="1492" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1443" class="Function">¬-elim</a> <a id="1499" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1499" class="Bound">¬x</a> <a id="1502" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1502" class="Bound">x</a> <a id="1504" class="Symbol">=</a> <a id="1506" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1499" class="Bound">¬x</a> <a id="1509" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#1502" class="Bound">x</a>{% endraw %}</pre>
Here we write `¬x` for evidence of `¬ A` and `x` for evidence of `A`.  This
means that `¬x` must be a function of type `A → ⊥`, and hence the application
`¬x x` must be of type `⊥`.  Note that this rule is just a special case of `→-elim`.

We set the precedence of negation so that it binds more tightly
than disjunction and conjunction, but less tightly than anything else.
<pre class="Agda">{% raw %}<a id="1910" class="Keyword">infix</a> <a id="1916" class="Number">3</a> <a id="1918" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬_</a>{% endraw %}</pre>
Thus, `¬ A × ¬ B` parses as `(¬ A) × (¬ B)` and `¬ m ≡ n` as `¬ (m ≡ n)`.

In _classical_ logic, we have that `A` is equivalent to `¬ ¬ A`.
As we discuss below, in Agda we use _intuitionistic_ logic, where
we have only half of this equivalence, namely that `A` implies `¬ ¬ A`.
<pre class="Agda">{% raw %}<a id="¬¬-intro"></a><a id="2223" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2223" class="Function">¬¬-intro</a> <a id="2232" class="Symbol">:</a> <a id="2234" class="Symbol">∀</a> <a id="2236" class="Symbol">{</a><a id="2237" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2237" class="Bound">A</a> <a id="2239" class="Symbol">:</a> <a id="2241" class="PrimitiveType">Set</a><a id="2244" class="Symbol">}</a>
  <a id="2248" class="Symbol">→</a> <a id="2250" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2237" class="Bound">A</a>
    <a id="2256" class="Comment">-----</a>
  <a id="2264" class="Symbol">→</a> <a id="2266" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="2268" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="2270" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2237" class="Bound">A</a>
<a id="2272" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2223" class="Function">¬¬-intro</a> <a id="2281" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2281" class="Bound">x</a> <a id="2283" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2283" class="Bound">¬x</a> <a id="2286" class="Symbol">=</a> <a id="2288" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2283" class="Bound">¬x</a> <a id="2291" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2281" class="Bound">x</a>{% endraw %}</pre>
Let `x` be evidence of `A`. We show that assuming
`¬ A` leads to a contradiction, and hence `¬ ¬ A` must hold.
Let `¬x` be evidence of `¬ A`.  Then from `A` and `¬ A`
we have a contradiction, evidenced by `¬x x`.  Hence, we have
shown `¬ ¬ A`.

We cannot show that `¬ ¬ A` implies `A`, but we can show that
`¬ ¬ ¬ A` implies `¬ A`.
<pre class="Agda">{% raw %}<a id="¬¬¬-elim"></a><a id="2649" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2649" class="Function">¬¬¬-elim</a> <a id="2658" class="Symbol">:</a> <a id="2660" class="Symbol">∀</a> <a id="2662" class="Symbol">{</a><a id="2663" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2663" class="Bound">A</a> <a id="2665" class="Symbol">:</a> <a id="2667" class="PrimitiveType">Set</a><a id="2670" class="Symbol">}</a>
  <a id="2674" class="Symbol">→</a> <a id="2676" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="2678" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="2680" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="2682" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2663" class="Bound">A</a>
    <a id="2688" class="Comment">-------</a>
  <a id="2698" class="Symbol">→</a> <a id="2700" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="2702" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2663" class="Bound">A</a>
<a id="2704" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2649" class="Function">¬¬¬-elim</a> <a id="2713" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2713" class="Bound">¬¬¬x</a> <a id="2718" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2718" class="Bound">x</a> <a id="2720" class="Symbol">=</a> <a id="2722" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2713" class="Bound">¬¬¬x</a> <a id="2727" class="Symbol">(</a><a id="2728" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2223" class="Function">¬¬-intro</a> <a id="2737" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#2718" class="Bound">x</a><a id="2738" class="Symbol">)</a>{% endraw %}</pre>
Let `¬¬¬x` be evidence of `¬ ¬ ¬ A`. We will show that assuming
`A` leads to a contradiction, and hence `¬ A` must hold.
Let `x` be evidence of `A`. Then by the previous result, we
can conclude `¬ ¬ A`, evidenced by `¬¬-intro x`.  Then from
`¬ ¬ ¬ A` and `¬ ¬ A` we have a contradiction, evidenced by
`¬¬¬x (¬¬-intro x)`.  Hence we have shown `¬ A`.

Another law of logic is _contraposition_,
stating that if `A` implies `B`, then `¬ B` implies `¬ A`.
<pre class="Agda">{% raw %}<a id="contraposition"></a><a id="3216" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3216" class="Function">contraposition</a> <a id="3231" class="Symbol">:</a> <a id="3233" class="Symbol">∀</a> <a id="3235" class="Symbol">{</a><a id="3236" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3236" class="Bound">A</a> <a id="3238" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3238" class="Bound">B</a> <a id="3240" class="Symbol">:</a> <a id="3242" class="PrimitiveType">Set</a><a id="3245" class="Symbol">}</a>
  <a id="3249" class="Symbol">→</a> <a id="3251" class="Symbol">(</a><a id="3252" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3236" class="Bound">A</a> <a id="3254" class="Symbol">→</a> <a id="3256" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3238" class="Bound">B</a><a id="3257" class="Symbol">)</a>
    <a id="3263" class="Comment">-----------</a>
  <a id="3277" class="Symbol">→</a> <a id="3279" class="Symbol">(</a><a id="3280" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="3282" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3238" class="Bound">B</a> <a id="3284" class="Symbol">→</a> <a id="3286" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="3288" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3236" class="Bound">A</a><a id="3289" class="Symbol">)</a>
<a id="3291" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3216" class="Function">contraposition</a> <a id="3306" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3306" class="Bound">f</a> <a id="3308" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3308" class="Bound">¬y</a> <a id="3311" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3311" class="Bound">x</a> <a id="3313" class="Symbol">=</a> <a id="3315" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3308" class="Bound">¬y</a> <a id="3318" class="Symbol">(</a><a id="3319" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3306" class="Bound">f</a> <a id="3321" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3311" class="Bound">x</a><a id="3322" class="Symbol">)</a>{% endraw %}</pre>
Let `f` be evidence of `A → B` and let `¬y` be evidence of `¬ B`.  We
will show that assuming `A` leads to a contradiction, and hence `¬ A`
must hold. Let `x` be evidence of `A`.  Then from `A → B` and `A` we
may conclude `B`, evidenced by `f x`, and from `B` and `¬ B` we may
conclude `⊥`, evidenced by `¬y (f x)`.  Hence, we have shown `¬ A`.

Using negation, it is straightforward to define inequality.
<pre class="Agda">{% raw %}<a id="_≢_"></a><a id="3754" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3754" class="Function Operator">_≢_</a> <a id="3758" class="Symbol">:</a> <a id="3760" class="Symbol">∀</a> <a id="3762" class="Symbol">{</a><a id="3763" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3763" class="Bound">A</a> <a id="3765" class="Symbol">:</a> <a id="3767" class="PrimitiveType">Set</a><a id="3770" class="Symbol">}</a> <a id="3772" class="Symbol">→</a> <a id="3774" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3763" class="Bound">A</a> <a id="3776" class="Symbol">→</a> <a id="3778" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3763" class="Bound">A</a> <a id="3780" class="Symbol">→</a> <a id="3782" class="PrimitiveType">Set</a>
<a id="3786" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3786" class="Bound">x</a> <a id="3788" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3754" class="Function Operator">≢</a> <a id="3790" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3790" class="Bound">y</a>  <a id="3793" class="Symbol">=</a>  <a id="3796" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="3798" class="Symbol">(</a><a id="3799" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3786" class="Bound">x</a> <a id="3801" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Equality.html#83" class="Datatype Operator">≡</a> <a id="3803" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3790" class="Bound">y</a><a id="3804" class="Symbol">)</a>{% endraw %}</pre>
It is trivial to show distinct numbers are not equal.
<pre class="Agda">{% raw %}<a id="3884" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3884" class="Function">_</a> <a id="3886" class="Symbol">:</a> <a id="3888" class="Number">1</a> <a id="3890" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3754" class="Function Operator">≢</a> <a id="3892" class="Number">2</a>
<a id="3894" class="Symbol">_</a> <a id="3896" class="Symbol">=</a> <a id="3898" class="Symbol">λ()</a>{% endraw %}</pre>
This is our first use of an absurd pattern in a lambda expression.
The type `M ≡ N` is occupied exactly when `M` and `N` simplify to
identical terms. Since `1` and `2` simplify to distinct normal forms,
Agda determines that there is no possible evidence that `1 ≡ 2`.
As a second example, it is also easy to validate
Peano's postulate that zero is not the successor of any number.
<pre class="Agda">{% raw %}<a id="peano"></a><a id="4307" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4307" class="Function">peano</a> <a id="4313" class="Symbol">:</a> <a id="4315" class="Symbol">∀</a> <a id="4317" class="Symbol">{</a><a id="4318" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4318" class="Bound">m</a> <a id="4320" class="Symbol">:</a> <a id="4322" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Nat.html#97" class="Datatype">ℕ</a><a id="4323" class="Symbol">}</a> <a id="4325" class="Symbol">→</a> <a id="4327" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Nat.html#115" class="InductiveConstructor">zero</a> <a id="4332" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#3754" class="Function Operator">≢</a> <a id="4334" href="https://agda.github.io/agda-stdlib/Agda.Builtin.Nat.html#128" class="InductiveConstructor">suc</a> <a id="4338" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4318" class="Bound">m</a>
<a id="4340" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4307" class="Function">peano</a> <a id="4346" class="Symbol">=</a> <a id="4348" class="Symbol">λ()</a>{% endraw %}</pre>
The evidence is essentially the same, as the absurd pattern matches
all possible evidence of type `zero ≡ suc m`.

Given the correspondence of implication to exponentiation and
false to the type with no members, we can view negation as
raising to the zero power.  This indeed corresponds to what
we know for arithmetic, where

    0 ^ n  ≡  1,  if n ≡ 0
           ≡  0,  if n ≢ 0

Indeed, there is exactly one proof of `⊥ → ⊥`.
<pre class="Agda">{% raw %}<a id="id"></a><a id="4805" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4805" class="Function">id</a> <a id="4808" class="Symbol">:</a> <a id="4810" href="https://agda.github.io/agda-stdlib/Data.Empty.html#243" class="Datatype">⊥</a> <a id="4812" class="Symbol">→</a> <a id="4814" href="https://agda.github.io/agda-stdlib/Data.Empty.html#243" class="Datatype">⊥</a>
<a id="4816" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4805" class="Function">id</a> <a id="4819" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4819" class="Bound">x</a> <a id="4821" class="Symbol">=</a> <a id="4823" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#4819" class="Bound">x</a>{% endraw %}</pre>
It is easy to see there are no possible values of type `A → ⊥`
unless `A` is equivalent to `⊥`.  We have that `⊥ → A`
always holds, by `⊥-elim`, and hence if `A → ⊥` holds then
`A` must be equivalent to `⊥`, in the sense that each implies
the other.



### Exercise (`≢`, `<-irrerflexive`)

Using negation, show that
[strict inequality]({{ site.baseurl }}{% link out/plfa/Relations.md %}/#strict-inequality)
is irreflexive, that is, `n < n` holds for no `n`.


### Exercise (`trichotomy`)

Show that strict inequality satisfies
[trichotomy]({{ site.baseurl }}{% link out/plfa/Relations.md %}/#trichotomy),
that is, for any naturals `m` and `n` exactly one of the following holds:

* `m < n`
* `m ≡ n`
* `m > n`

Here "exactly one" means that one of the three must hold, and each implies the
negation of the other two.


### Exercise (`⊎-dual-×`)

Show that conjunction, disjunction, and negation are related by a
version of De Morgan's Law.
<pre class="Agda">{% raw %}<a id="5790" class="Keyword">postulate</a>
  <a id="⊎-dual-×"></a><a id="5802" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5802" class="Postulate">⊎-dual-×</a> <a id="5811" class="Symbol">:</a> <a id="5813" class="Symbol">∀</a> <a id="5815" class="Symbol">{</a><a id="5816" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5816" class="Bound">A</a> <a id="5818" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5818" class="Bound">B</a> <a id="5820" class="Symbol">:</a> <a id="5822" class="PrimitiveType">Set</a><a id="5825" class="Symbol">}</a> <a id="5827" class="Symbol">→</a> <a id="5829" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="5831" class="Symbol">(</a><a id="5832" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5816" class="Bound">A</a> <a id="5834" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="5836" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5818" class="Bound">B</a><a id="5837" class="Symbol">)</a> <a id="5839" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}#4128" class="Record Operator">≃</a> <a id="5841" class="Symbol">(</a><a id="5842" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="5844" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5816" class="Bound">A</a><a id="5845" class="Symbol">)</a> <a id="5847" href="https://agda.github.io/agda-stdlib/Data.Product.html#1329" class="Function Operator">×</a> <a id="5849" class="Symbol">(</a><a id="5850" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="5852" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#5818" class="Bound">B</a><a id="5853" class="Symbol">)</a>{% endraw %}</pre>
This result is an easy consequence of something we've proved previously.

Is there also a term of the following type?
<pre class="Agda">{% raw %}<a id="5997" class="Keyword">postulate</a>
  <a id="×-dual-⊎"></a><a id="6009" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6009" class="Postulate">×-dual-⊎</a> <a id="6018" class="Symbol">:</a> <a id="6020" class="Symbol">∀</a> <a id="6022" class="Symbol">{</a><a id="6023" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6023" class="Bound">A</a> <a id="6025" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6025" class="Bound">B</a> <a id="6027" class="Symbol">:</a> <a id="6029" class="PrimitiveType">Set</a><a id="6032" class="Symbol">}</a> <a id="6034" class="Symbol">→</a> <a id="6036" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="6038" class="Symbol">(</a><a id="6039" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6023" class="Bound">A</a> <a id="6041" href="https://agda.github.io/agda-stdlib/Data.Product.html#1329" class="Function Operator">×</a> <a id="6043" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6025" class="Bound">B</a><a id="6044" class="Symbol">)</a> <a id="6046" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Isomorphism.md %}{% raw %}#4128" class="Record Operator">≃</a> <a id="6048" class="Symbol">(</a><a id="6049" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="6051" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6023" class="Bound">A</a><a id="6052" class="Symbol">)</a> <a id="6054" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="6056" class="Symbol">(</a><a id="6057" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="6059" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#6025" class="Bound">B</a><a id="6060" class="Symbol">)</a>{% endraw %}</pre>
If so, prove; if not, explain why.


## Intuitive and Classical logic

In Gilbert and Sullivan's _The Gondoliers_, Casilda is told that
as an infant she was married to the heir of the King of Batavia, but
that due to a mix-up no one knows which of two individuals, Marco or
Giuseppe, is the heir.  Alarmed, she wails "Then do you mean to say
that I am married to one of two gondoliers, but it is impossible to
say which?"  To which the response is "Without any doubt of any kind
whatever."

Logic comes in many varieties, and one distinction is between
_classical_ and _intuitionistic_. Intuitionists, concerned
by assumptions made by some logicians about the nature of
infinity, insist upon a constructionist notion of truth.  In
particular, they insist that a proof of `A ⊎ B` must show
_which_ of `A` or `B` holds, and hence they would reject the
claim that Casilda is married to Marco or Giuseppe until one of the
two was identified as her husband.  Perhaps Gilbert and Sullivan
anticipated intuitionism, for their story's outcome is that the heir
turns out to be a third individual, Luiz, with whom Casilda is,
conveniently, already in love.

Intuitionists also reject the law of the excluded middle, which
asserts `A ⊎ ¬ A` for every `A`, since the law gives no clue as to
_which_ of `A` or `¬ A` holds. Heyting formalised a variant of
Hilbert's classical logic that captures the intuitionistic notion of
provability. In particular, the law of the excluded middle is provable
in Hilbert's logic, but not in Heyting's.  Further, if the law of the
excluded middle is added as an axiom to Heyting's logic, then it
becomes equivalent to Hilbert's.  Kolmogorov showed the two logics
were closely related: he gave a double-negation translation, such that
a formula is provable in classical logic if and only if its
translation is provable in intuitionistic logic.

Propositions as Types was first formulated for intuitionistic logic.
It is a perfect fit, because in the intuitionist interpretation the
formula `A ⊎ B` is provable exactly when one exhibits either a proof
of `A` or a proof of `B`, so the type corresponding to disjunction is
a disjoint sum.

(Parts of the above are adopted from "Propositions as Types", Philip Wadler,
_Communications of the ACM_, December 2015.)

## Excluded middle is irrefutable

The law of the excluded middle can be formulated as follows.
<pre class="Agda">{% raw %}<a id="8463" class="Keyword">postulate</a>
  <a id="em"></a><a id="8475" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8475" class="Postulate">em</a> <a id="8478" class="Symbol">:</a> <a id="8480" class="Symbol">∀</a> <a id="8482" class="Symbol">{</a><a id="8483" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8483" class="Bound">A</a> <a id="8485" class="Symbol">:</a> <a id="8487" class="PrimitiveType">Set</a><a id="8490" class="Symbol">}</a> <a id="8492" class="Symbol">→</a> <a id="8494" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8483" class="Bound">A</a> <a id="8496" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="8498" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="8500" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8483" class="Bound">A</a>{% endraw %}</pre>
As we noted, the law of the excluded middle does not hold in
intuitionistic logic.  However, we can show that it is _irrefutable_,
meaning that the negation of its negation is provable (and hence that
its negation is never provable).
<pre class="Agda">{% raw %}<a id="em-irrefutable"></a><a id="8760" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8760" class="Function">em-irrefutable</a> <a id="8775" class="Symbol">:</a> <a id="8777" class="Symbol">∀</a> <a id="8779" class="Symbol">{</a><a id="8780" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8780" class="Bound">A</a> <a id="8782" class="Symbol">:</a> <a id="8784" class="PrimitiveType">Set</a><a id="8787" class="Symbol">}</a> <a id="8789" class="Symbol">→</a> <a id="8791" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="8793" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="8795" class="Symbol">(</a><a id="8796" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8780" class="Bound">A</a> <a id="8798" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="8800" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="8802" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8780" class="Bound">A</a><a id="8803" class="Symbol">)</a>
<a id="8805" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8760" class="Function">em-irrefutable</a> <a id="8820" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8820" class="Bound">k</a> <a id="8822" class="Symbol">=</a> <a id="8824" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8820" class="Bound">k</a> <a id="8826" class="Symbol">(</a><a id="8827" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#495" class="InductiveConstructor">inj₂</a> <a id="8832" class="Symbol">λ{</a> <a id="8835" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8835" class="Bound">x</a> <a id="8837" class="Symbol">→</a> <a id="8839" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8820" class="Bound">k</a> <a id="8841" class="Symbol">(</a><a id="8842" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#470" class="InductiveConstructor">inj₁</a> <a id="8847" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#8835" class="Bound">x</a><a id="8848" class="Symbol">)</a> <a id="8850" class="Symbol">})</a>{% endraw %}</pre>
The best way to explain this code is to develop it interactively.

    em-irrefutable k = ?

Given evidence `k` that `¬ (A ⊎ ¬ A)`, that is, a function that give a
value of type `A ⊎ ¬ A` returns a value of the empty type, we must fill
in `?` with a term that returns a value of the empty type.  The only way
we can get a value of the empty type is by applying `k` itself, so let's
expand the hole accordingly.

    em-irrefutable k = k ?

We need to fill the new hole with a value of type `A ⊎ ¬ A`. We don't have
a value of type `A` to hand, so let's pick the second disjunct.

    em-irrefutable k = k (inj₂ λ{ x → ? })

The second disjunct accepts evidence of `¬ A`, that is, a function
that given a value of type `A` returns a value of the empty type.  We
bind `x` to the value of type `A`, and now we need to fill in the hole
with a value of the empty type.  Once again, the only way we can get a
value of the empty type is by applying `k` itself, so let's expand the
hole accordingly.

    em-irrefutable k = k (inj₂ λ{ x → k ? })

This time we do have a value of type `A` to hand, namely `x`, so we can
pick the first disjunct.

    em-irrefutable k = k (inj₂ λ{ x → k (inj₁ x) })

There are no holes left! This completes the proof.

The following story illustrates the behaviour of the term we have created.
(With apologies to Peter Selinger, who tells a similar story
about a king, a wizard, and the Philosopher's stone.)

Once upon a time, the devil approached a man and made an offer:
"Either (a) I will give you one billion dollars, or (b) I will grant
you any wish if you pay me one billion dollars.
Of course, I get to choose whether I offer (a) or (b)."

The man was wary.  Did he need to sign over his soul?
No, said the devil, all the man need do is accept the offer.

The man pondered.  If he was offered (b) it was unlikely that he would
ever be able to buy the wish, but what was the harm in having the
opportunity available?

"I accept," said the man at last.  "Do I get (a) or (b)?"

The devil paused.  "I choose (b)."

The man was disappointed but not surprised.  That was that, he thought.
But the offer gnawed at him.  Imagine what he could do with his wish!
Many years passed, and the man began to accumulate money.  To get the
money he sometimes did bad things, and dimly he realised that
this must be what the devil had in mind.
Eventually he had his billion dollars, and the devil appeared again.

"Here is a billion dollars," said the man, handing over a valise
containing the money.  "Grant me my wish!"

The devil took possession of the valise.  Then he said, "Oh, did I say
(b) before?  I'm so sorry.  I meant (a).  It is my great pleasure to
give you one billion dollars."

And the devil handed back to the man the same valise that the man had
just handed to him.

(Parts of the above are adopted from "Call-by-Value is Dual to Call-by-Name",
Philip Wadler, _International Conference on Functional Programming_, 2003.)


#### Exercise

Consider the following five terms of the given types.
<pre class="Agda">{% raw %}<a id="11902" class="Keyword">postulate</a>
  <a id="em′"></a><a id="11914" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11914" class="Postulate">em′</a>         <a id="11926" class="Symbol">:</a> <a id="11928" class="Symbol">∀</a> <a id="11930" class="Symbol">{</a><a id="11931" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11931" class="Bound">A</a> <a id="11933" class="Symbol">:</a> <a id="11935" class="PrimitiveType">Set</a><a id="11938" class="Symbol">}</a> <a id="11940" class="Symbol">→</a> <a id="11942" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11931" class="Bound">A</a> <a id="11944" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="11946" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="11948" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11931" class="Bound">A</a>
  <a id="¬¬-elim"></a><a id="11952" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11952" class="Postulate">¬¬-elim</a>     <a id="11964" class="Symbol">:</a> <a id="11966" class="Symbol">∀</a> <a id="11968" class="Symbol">{</a><a id="11969" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11969" class="Bound">A</a> <a id="11971" class="Symbol">:</a> <a id="11973" class="PrimitiveType">Set</a><a id="11976" class="Symbol">}</a> <a id="11978" class="Symbol">→</a> <a id="11980" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="11982" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="11984" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11969" class="Bound">A</a> <a id="11986" class="Symbol">→</a> <a id="11988" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11969" class="Bound">A</a>
  <a id="peirce"></a><a id="11992" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#11992" class="Postulate">peirce</a>      <a id="12004" class="Symbol">:</a> <a id="12006" class="Symbol">∀</a> <a id="12008" class="Symbol">{</a><a id="12009" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12009" class="Bound">A</a> <a id="12011" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12011" class="Bound">B</a> <a id="12013" class="Symbol">:</a> <a id="12015" class="PrimitiveType">Set</a><a id="12018" class="Symbol">}</a> <a id="12020" class="Symbol">→</a> <a id="12022" class="Symbol">(((</a><a id="12025" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12009" class="Bound">A</a> <a id="12027" class="Symbol">→</a> <a id="12029" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12011" class="Bound">B</a><a id="12030" class="Symbol">)</a> <a id="12032" class="Symbol">→</a> <a id="12034" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12009" class="Bound">A</a><a id="12035" class="Symbol">)</a> <a id="12037" class="Symbol">→</a> <a id="12039" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12009" class="Bound">A</a><a id="12040" class="Symbol">)</a>
  <a id="→-implies-⊎"></a><a id="12044" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12044" class="Postulate">→-implies-⊎</a> <a id="12056" class="Symbol">:</a> <a id="12058" class="Symbol">∀</a> <a id="12060" class="Symbol">{</a><a id="12061" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12061" class="Bound">A</a> <a id="12063" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12063" class="Bound">B</a> <a id="12065" class="Symbol">:</a> <a id="12067" class="PrimitiveType">Set</a><a id="12070" class="Symbol">}</a> <a id="12072" class="Symbol">→</a> <a id="12074" class="Symbol">(</a><a id="12075" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12061" class="Bound">A</a> <a id="12077" class="Symbol">→</a> <a id="12079" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12063" class="Bound">B</a><a id="12080" class="Symbol">)</a> <a id="12082" class="Symbol">→</a> <a id="12084" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12086" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12061" class="Bound">A</a> <a id="12088" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="12090" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12063" class="Bound">B</a>
  <a id="×-implies-⊎"></a><a id="12094" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12094" class="Postulate">×-implies-⊎</a> <a id="12106" class="Symbol">:</a> <a id="12108" class="Symbol">∀</a> <a id="12110" class="Symbol">{</a><a id="12111" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12111" class="Bound">A</a> <a id="12113" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12113" class="Bound">B</a> <a id="12115" class="Symbol">:</a> <a id="12117" class="PrimitiveType">Set</a><a id="12120" class="Symbol">}</a> <a id="12122" class="Symbol">→</a> <a id="12124" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12126" class="Symbol">(</a><a id="12127" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12111" class="Bound">A</a> <a id="12129" href="https://agda.github.io/agda-stdlib/Data.Product.html#1329" class="Function Operator">×</a> <a id="12131" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12113" class="Bound">B</a><a id="12132" class="Symbol">)</a> <a id="12134" class="Symbol">→</a> <a id="12136" class="Symbol">(</a><a id="12137" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12139" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12111" class="Bound">A</a><a id="12140" class="Symbol">)</a> <a id="12142" href="https://agda.github.io/agda-stdlib/Data.Sum.Base.html#414" class="Datatype Operator">⊎</a> <a id="12144" class="Symbol">(</a><a id="12145" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12147" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12113" class="Bound">B</a><a id="12148" class="Symbol">)</a>{% endraw %}</pre>
Show that given any one term of the specified type, we can derive the others.


### Exercise (`¬-stable`, `×-stable`)

Say that a formula is _stable_ if double negation elimination holds for it.
<pre class="Agda">{% raw %}<a id="Stable"></a><a id="12369" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12369" class="Function">Stable</a> <a id="12376" class="Symbol">:</a> <a id="12378" class="PrimitiveType">Set</a> <a id="12382" class="Symbol">→</a> <a id="12384" class="PrimitiveType">Set</a>
<a id="12388" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12369" class="Function">Stable</a> <a id="12395" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12395" class="Bound">A</a> <a id="12397" class="Symbol">=</a> <a id="12399" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12401" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12403" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12395" class="Bound">A</a> <a id="12405" class="Symbol">→</a> <a id="12407" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12395" class="Bound">A</a>{% endraw %}</pre>
Show that any negated formula is stable, and that the conjunction
of two stable formulas is stable.
<pre class="Agda">{% raw %}<a id="12533" class="Keyword">postulate</a>

  <a id="¬-stable"></a><a id="12546" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12546" class="Postulate">¬-stable</a> <a id="12555" class="Symbol">:</a> <a id="12557" class="Symbol">∀</a> <a id="12559" class="Symbol">{</a><a id="12560" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12560" class="Bound">A</a> <a id="12562" class="Symbol">:</a> <a id="12564" class="PrimitiveType">Set</a><a id="12567" class="Symbol">}</a>
      <a id="12575" class="Comment">------------</a>
    <a id="12592" class="Symbol">→</a> <a id="12594" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12369" class="Function">Stable</a> <a id="12601" class="Symbol">(</a><a id="12602" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#846" class="Function Operator">¬</a> <a id="12604" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12560" class="Bound">A</a><a id="12605" class="Symbol">)</a>

  <a id="×-stable"></a><a id="12610" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12610" class="Postulate">×-stable</a> <a id="12619" class="Symbol">:</a> <a id="12621" class="Symbol">∀</a> <a id="12623" class="Symbol">{</a><a id="12624" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12624" class="Bound">A</a> <a id="12626" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12626" class="Bound">B</a> <a id="12628" class="Symbol">:</a> <a id="12630" class="PrimitiveType">Set</a><a id="12633" class="Symbol">}</a>
    <a id="12639" class="Symbol">→</a> <a id="12641" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12369" class="Function">Stable</a> <a id="12648" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12624" class="Bound">A</a>
    <a id="12654" class="Symbol">→</a> <a id="12656" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12369" class="Function">Stable</a> <a id="12663" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12626" class="Bound">B</a>
      <a id="12671" class="Comment">--------------</a>
    <a id="12690" class="Symbol">→</a> <a id="12692" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12369" class="Function">Stable</a> <a id="12699" class="Symbol">(</a><a id="12700" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12624" class="Bound">A</a> <a id="12702" href="https://agda.github.io/agda-stdlib/Data.Product.html#1329" class="Function Operator">×</a> <a id="12704" href="{% endraw %}{{ site.baseurl }}{% link out/plfa/Negation.md %}{% raw %}#12626" class="Bound">B</a><a id="12705" class="Symbol">)</a>{% endraw %}</pre>

## Standard Prelude

Definitions similar to those in this chapter can be found in the standard library.
<pre class="Agda">{% raw %}<a id="12836" class="Keyword">import</a> <a id="12843" href="https://agda.github.io/agda-stdlib/Relation.Nullary.html" class="Module">Relation.Nullary</a> <a id="12860" class="Keyword">using</a> <a id="12866" class="Symbol">(</a><a id="12867" href="https://agda.github.io/agda-stdlib/Relation.Nullary.html#464" class="Function Operator">¬_</a><a id="12869" class="Symbol">)</a>
<a id="12871" class="Keyword">import</a> <a id="12878" href="https://agda.github.io/agda-stdlib/Relation.Nullary.Negation.html" class="Module">Relation.Nullary.Negation</a> <a id="12904" class="Keyword">using</a> <a id="12910" class="Symbol">(</a><a id="12911" href="https://agda.github.io/agda-stdlib/Relation.Nullary.Negation.html#688" class="Function">contraposition</a><a id="12925" class="Symbol">)</a>{% endraw %}</pre>

## Unicode

This chapter uses the following unicode.

    ¬  U+00AC  NOT SIGN (\neg)
