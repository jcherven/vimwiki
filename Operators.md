# Java Basics

## Operators

Understanding variables in Java is pretty important, but you should also know
how to do something with them. Like any other language, Java supports a large
number of operators that perform mathematical or logical operations on
variables. 

You already know the main one: the assignment operator, or equals-sign. This
operator takes whatever is on the right side of the operator, and stores it in
the variable on the left side. Now, we say this is a right-to-left operator,
because in order to work it must first compute the value on the right hand side
before it can store it in the left – but the process of that computation works
left to right. Moreover, there are some rules of precedence! 

Parenthesis, array indices, dot: `() [] .`
Postfix: `++ --`
Multiplicative: `* / %`
Additive: `+ -`
Shift: `<< >> >>>`
Relational: `< > <= >= instanceof`
Equality: `== !=`
Bitwise: `& ^ |`
Logical: `&& ||`
Ternary: `expr?expr:expr`
Assignment: `= += -= *= /= %=`
            `&= ^= \=`
            `<<= >>= >>>=`

Here’s a quick list of all the operators, in order of precedence: 

First, parenthesis work just like they do in mathematical equations – you
compute the values inside parenthesis before those outside. 

Then you have the postfix operators, ++ and --. These operators add one or
subtract one from the expression provided. If I have an int variable named ‘a’,
I can say a++, and that’s the same as saying a = a + 1. Ditto for a--. I could
also put the ++ or -- before the expression, like ++a. The difference between a
postfix operator and these prefix operators comes up when they are part of a
larger expression – in which case a++ will evaluate after the expression is
done, while ++a evaluates before it. As an example, if I have int a = 4, and I
have the expression System. out. println(++a), that will print 5 to the
console, whereas a++ would print 4 and then increment the value of a after
printing. 

Then you have the multiplicative operators, * for multiplication, / for
division, and % for modulus. If you haven’t taken an advanced algebra course,
you’re probably not that familiar with the modulus operator – it returns the
remainder of a division result. Bytes, Shorts, Ints and Longs in Java only
store whole numbers, which means that when division occurs, you get a result
and a remainder. When dividing with the ‘/’ operator, you get the result of
integer division. If you use the ‘%’ operator, you get the remainder instead. 

The additive operators should be pretty obvious. But after those come the shift
operators, which work on the binary value of a primitive type’s value. These
shift the digits of the binary representation of a value left or right a
certain number of spaces, resulting in a different value. 

The relational operators compare two values and return a boolean result. These
are ‘<’, ‘>’, ‘<=’, ‘>=’, and “instanceof”. 

That last one determines if the object pointed to by a reference variable is an
instance of a certain class, and we’ll talk more about it in another video. You
also have the equality operators, == and !=. Don’t confuse the equality
operator with the assignment operator!These operators compare two values to
determine if they are equal or not-equal respectively. 

Next you have the bitwise operators, used to manipulate the binary
representation of values. You have bitwise AND (&), bitwise exclusive OR (^),
and bitwise inclusive OR (|). These shouldn’t be confused with the logical &&
and logical || operators. These operators join two other boolean expressions to
produce a new boolean result. For example, I might have a statement like a > 3
|| a <= 2. 

You can also use the ternary operator to construct a quick If-Then-Else
conditional statement. We’ll talk more about those in another video, but it
works like this: You use the operator with three expressions – the first and
second are divided by a ‘?’, the second and third are divided by a ‘:’. The
first expression must be a boolean expression, and it is followed by a ‘?’. If
the boolean expression is true, the second statement will execute. If the first
expression is false, the third statement will execute. 

The operator with the lowest precedence is of course the assignment operator,
because every other operator must be used to calculate a value that gets
assigned. 

But more advanced than our humble assignment operator, are the
arithmetic-assignment combo operators. These operators are the same as applying
an expression on the right side of the assignment operator to the variable on
the left, and storing the result back into the same variable. For example,
saying a += 3 is the same as saying a = a + 3. This adds 3 to the value of a,
and stores the new value in the variable named ‘a’. 

And that’s it. Armed with these operators, you can now go out and create some
very basic Java programs. But if you want to know more, stay tuned. 

< Variables and Data Types | Statements >

