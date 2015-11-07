Exercise. Implement the Maybe type using the composite pattern
--------------------------------------------------------------

Hint. Cheat from the provided immutable-list implementations. 

*** Modify the given files Nothing.java and Just.java.
*** You lose all marks if you modify any of the other given files.

You are free to create your own files for testing, which you may
include in the submission.

------------
Introduction
------------

We begin by doing something people often do, but that it is unsafe and
the cause of several programming errors, and hence should be
avoided. We use the suffix "_" for methods that rely on bad practice,
and remove it from their versions that apply better practice.

https://en.wikipedia.org/wiki/Pointer_%28computer_programming%29#Null_pointer
https://en.wikipedia.org/wiki/Tony_Hoare#Apologies_and_retractions

Find an element of the array as satisfying the predicate p, if such an
element exists, and null otherwise:

  static <A> A find_(Predicate<A> p, A [] as) {
    for (A a : as) {
      if (p.holds(a))
        return a; 
    } 
    // If the for-loop ends, this means we haven't found anything.
    return null;
  }

Now this is very likely to cause a null-pointer exception.
In the following method, it doesn't.

  static <A> boolean some_(Predicate<A> p, A [] as) {
    return find(p, as) != null;
  }

A better-engineered solution is to use the Maybe type. The Maybe<A>
type has two kinds of elements:

  Maybe<Integer> x = new Nothing<Integer>(); // Get nothing
  Maybe<Integer> y = new Just<Integer>(17);  // Get 17

You may think of the Maybe type as the type of lists that can have
zero or one elements, if you wish.

I think of Maybe<A> as maybe giving just an element of type A, and
maybe nothing.

Find just an element of the array as satisfying the predicate p, if
such an element exists, and nothing otherwise.

  static <A> Maybe<A> find(Predicate<A> p, A [] as) {
    for (A a : as) {
      if (p.holds(a))
        return new Just<A>(a); 
    } 
    // If the for-loop ends, this means we haven't found anything.
    return new Nothing<A>();
  }
    
  static <A> boolean some(Predicate<A> p, A [] as) {
    return !find(p, as).isNothing();
  }

As another example, the unsafe head and tail operations in the
interface IList could have been given the following types:
  //
  public <A> Maybe<A> head();
  public <A> Maybe<IList<A>> tail();

--------------------------------
The Maybe interface given to you
--------------------------------

Interface for the Maybe type using the "composite pattern".  We
include high-order methods.  We will use A,B,C for type variables.

public interface Maybe<A> {
  public boolean isNothing();
  public int     size();         
  public boolean has(A a);            
  // Usafe:
  public A fromMaybe();  
  // Higher-order methods:
  public Maybe<A> filter(Predicate<A> p);     
  public <B> Maybe<B> map(Function<A,B> f);   
  public <B> B fold(Function<A,B> f, B b); 
  public boolean all(Predicate<A> p);         
  public boolean some(Predicate<A> p);       
  public void forEach(Action<A> a);          
} 

Your should fill in the classes Nothing and Just that implement this
interface. Read further instructions there. 

To understand what these methods ought to do, see the SampleUsage file.

To check whether you have implemented them properly, run SampleUsage,
and compare your output to the output quoted inside the file within
comments.

------
Submit
------

A zip file to Canvas with the file-tree structure

  Maybe-exercise
    clean
    compile
    readme.txt
    run
    maybe
     Action.java    
     Function.java  
     Maybe.java    
     Predicate.java  
     SampleUsage.java
     Exercise.java    <--- Don't change this or any file above this.
     Just.java        <--- You should ONLY change this  
     Nothing.java     <--- and this.

To lose all marks, please change any of the files you are not supposed
to change.

You may add new test files without losing marks. We will mark Just and
Nothing only.

END.


