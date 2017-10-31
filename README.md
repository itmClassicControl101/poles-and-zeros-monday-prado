% Poles And Zeros by Inspection: Sample repository for Session 2 in Classic Control Theory 101
% Instituto Tecnológico de Morelia
% October 2017
# Laboratory session 2: Poles and zeros found by Inspection
## Introduction

During third unit classes, students will learn that poles and zeros can be found by solving the roots of the transfer function. During the process, the better way to identify poles and zeros should be by rearranging the transfer function in a factored way. However, the most complicated part of the methodology is to obtain the transfer function equation. During this session students must learn how to write the transfer function just by looking at the network arrangement; by inspection[^1]. 

## Example 
If we understand that a transfer function links an output signal (the response) to an input signal (the excitation), then a zero at a particular frequency prevents the excitation from reaching the output. Let us try to apply this  theory to the passive filter appearing in the Figure:

->![Figure 1: First order system](file:///Users/Marx/Dropbox/Docencia/Clases/2017/semester2/Control%20I/labSessions/session2/circuit.png)<-

Notice that an ac source $$(V_{in} )$$ is delivering a signal through a resistor $$ R_1 $$ to a network made of a series-parallel combination of two resistors and a capacitor. There is one distinct storage element $$ C_1 $$ ; this is a first-order network. Nevertheless, is difficult to know where there are poles or zeros, however, it must fit the format given by:

$$ H(s)=\frac{V_{in}(s)}{V_{out}(s)}=G_0\frac{1+s/\omega_{z1}}{1+s/\omega_{p1}} $$

### DC point
There is possible to obtain by "brute-force" the expression of impedance $$ Z_1 $$ and applying the voltage divider expression:

$$ V_{out}(s)=V_{in}(s) \frac{Z_1}{Z_1+R_1}$$

Students can use several ways to obtain the final expression, but maybe will end up with a moderately complicated expression and the chances to make mistakes during the expansions are real. Furthermore, without additional work on the final result, it is unlikely that poles and zeros pop up at the end.

**In order to start the derivation**, observe the system at dc, when $$ s = 0 $$. This is exactly what *SPICE* does when it starts the simulation: to calculate the dc operating point of the circuit under study, also called the **bias point**, *SPICE* **opens all capacitors and shorts all inductors**. With the equivalent network, it calculates all dc currents and voltages that the simulator will use for the rest of the simulation. In the network, it is possible to do the same. When $$ C_1 $$ is open, are left with $$ R_1 $$ and $$ R_3 $$. Therefore, the dc attenuation $$ G_0 $$ is:

$$ G_0=\frac{R_3}{R_1+R_3} $$


->![Equivalent circuit to obtain the DC operating point￼](file:///Users/Marx/Dropbox/Docencia/Clases/2017/semester2/Control%20I/labSessions/session2/circuitDc.jpg =268x344)<-


Now, recalling the definition of a zero, it is a frequency point at which the excitation no longer reaches the output. In Figure 1, **what element in the input signal path can stop its propagation?** 

Either an element in series with the signal offers an infinite impedance at a certain frequency or an element linking the signal path to the ground becomes a short circuit, again at a certain frequency point. In our example, the only element that can stop the signal from reaching the output is the series combination of $$ R_2 $$ and $$ C_1 $$. When its resulting impedance is null (**short circuit**), we have a zero in the transfer function:
 
$$ R_2+\frac{1}{1+sC_1}=0 $$

$$ \omega_{z1}=\frac{1}{R_2C_1} $$


Now our partial transfer function is:

$$ H(s)=G_0\frac{N(s)}{D(s)}=\frac{R_3}{R_1+R_3}\frac{1+sR_2C_1}{D(s)} $$

However the poles still hide in the $$D(s) $$.

### Poles, zeros and time constants

By definition, the gain is a dimensionless expression. When you say the voltage gain of a system is $$ 20 dB $$, it is another means to say that the gain is $$ 10 V/V $$ or $$ 10 $$. A term multiplied by s has the dimension of a frequency, $$ Hz $$. A term multiplied by $$ s^2 $$ has a dimension of a squared frequency, $$ Hz^2 $$. To make sure that all $$ s $$-terms and $$ s^2 $$-terms lose their dimension when multiplied by a coefficient, these coefficients must have the inverse dimension.[^2] 

How to get the poles then? We need to identify the time constants of our system but in a different manner than what we have shown for the zeros. As we stated, the transfer function denominator $$ D(s) $$ of a linear network does not depend on its excitation or response signals. It only depends on the network structure alone. If you look at transfer functions describing a given network, its output impedance, its input admittance, and so on, then you will see that all these equations share a common denominator $$ D(s) $$.

To study the network alone, we are going to bring its excitation signal to zero. If the excitation signal is a voltage source, we set it to zero: replace it by a short circuit. If the excitation signal is a current source, then open circuit it. Let’s apply this technique to Figure 1 by shorting to ground the left terminal of $$ R_1 $$:


->![title](file:///Users/Marx/Dropbox/Docencia/Clases/2017/semester2/Control%20I/labSessions/session2/circuitDc.png)<-

The time constant is easily calculated by evaluating the resistance **seen** from the capacitor terminals. The first one is obviously $$ R_2 $$, in series with the parallel combination of $$ R_1 $$ and $$ R_3 $$:

$$ R=R_2+R_1 \parallel R_3 $$

The pole definition, for this simple first-order system, is simply the inverse of the equivalent time constant:

$$ \omega_{p1}=\frac{1}{\tau}=\frac{1}{RC_1}=(R_2+R_1 \parallel R_3)C_1 $$

The expression of our denominator D(s) is therefore
$$ D(s)=1+s/\omega_{p1} $$

The complete transfer function then becomes

$$ H(s)=G_0\frac{N(s)}{D(s)}=\frac{R_3}{R_1+R_3}\frac{1+sR_2C_1}{1+s(R_2+R_1 \parallel R_3)C_1}=G_0 \frac{1+s/\omega_{z1}}{1+s/\omega_{p1}}$$

This is what is called a low-entropy equation by analogy to thermodynamic laws. Simply put, the entropy of a system qualifies its degree of internal disorder.

## Part I

- For the part I obtain the transfer function (low-entropy TF) by inspection for the following circuit.
- Obtain the TF (high entropy) using common algebra techniques.
- The using your function developed in **Scilab** or **Matlab** check the response.

->![Circuit for part I](file:///Users/Marx/Dropbox/Docencia/Clases/2017/semester2/Control%20I/labSessions/session2/circuitPart1.png)<-

## Part II

For the next session get installed Spice(LTI Spice) to check the time response of the circuit. 
**Note: please read a little bit about the Spice programming language**

## Part III

This session will be carried out in the laboratory, thus get your own componentes to build your circuit in the proto-board, then:
 
- Measure the time response.
- Obtain the frequency response by evaluating up-to 8 points by decade, consider that each measurement must be take at steady-state conditions using an oscilloscope (RMS value)
- Graph the bode plot using your points
- Write your technical report and compare time response, frequency response and cut-off frequency. 

## References and footnotes 

[^1]: Designing Control Loops for Linear and Switching Power Supplies: A Tutorial Guide Power Supplie. Christophe Basso, Copyright: 2015,Pages: 590, ISBN: 9781608075577. 

[^2]: Therefore, the terms b1/b0 and a1/a0 must have a dimension of Hz−1, whereas the terms b2/b0 and a2/a0 must have a dimension of Hz−2. What offers a dimension of Hz−2 or actually seconds? A time constant does. What has a dimension of Hz−2 or squared seconds? A product of time constants. And this makes sense when you consider the expression of the zero found in (2.42); it has indeed the dimension of a time constant.   
