java cFN6806: Object Oriented Programming II
Problems - Set 3
Question 3-1
Implement Vasicek model for interest rate simulation

• Use Euler-Maruyama method to generate the paths. returned value is a tuple: 1) the end
rates of all paths, 2) the sum of all rates of all paths (except the starting   0
).
• You could use either vector or valarray for the result.
auto vasicek(double sd, double kappa, double r_mean, double r0,
double T, int paths, int steps, mt19937 gen) {
double dt = T / steps;
vector sum_rates(paths);
vector end_rates(paths);
^^.
return make_tuple(end_rates, sum_rates);
}
auto vasicek_valarray(double sd, double kappa, double r_mean,
double r0, double T, int paths, int steps, mt19937 gen) {
double dt = T / steps;
valarray sum_rates(0.0, paths);
valarray end_rates(r0, paths);
^^.
return make_tuple(end_rates, sum_rates);
}
• Below is my test code and result as reference. You could adapt it to test your result.
seed_seq seed{90127};
auto mtgen = mt19937{seed};
auto [end_rates, sum_rates] =
vasicek(sd, kappa, r_mean, r0, T, 20'000, int(0.5 * 365),
mtgen);
auto end_rates_avg =
accumulate(end_rates.begin(), end_rates.end(), 0.0) /
end_rates.size();
1auto sum_rates_avg =
accumulate(sum_rates.begin(), sum_rates.end(), 0.0) /
sum_rates.size();
cout ^ Open and sell signal whenever Close
< Open, and porformance metric is the 1-day lagged signal times the return of the next day
(assuming buy at next day Open). It’s fast to implement such backtesting. However, if we want
to simulate for adding the number of orders when we have 2nd buy signal, we need to modify
the algorithm but it will not be easy. Vectorized method can not simulate the execution of
orders realistically. At all, it is a simpliffed approach towards backtesting.
The event-driven approach is more sophiscated as it simulates the strategy as if it was executed
in real-time. The price series are loaded as a s代 写FN6806、c/c++，Python
代做程序编程语言tream of ticks and the strategy is executed on
each tick, and various modules can be added at both sides: the exeuction side and the strategy
 side. For example, the exeuction could simulation the price slippage of the execution, the
strategy side could simulate for stop loss and dynamic order sizing depends on past performance.
The event-driven approach is more ffexible and more realistic, but it is more difffcult
to implement.
In this exercise, you will read the source code of an event-driven simulator and try to understand
 how it works. You will need to document 5 places that exception could occur, what is the
error message, what could be the cause of the error and what could be the exception handling.
Create a ffle exceptions.txt and write down your answers.
This project will also be used in the Final quiz, so you should get familiar with it.
About the simulator:
• The author of this repo only made a start so it’s just a partial implementation. You would
ffnd many rough edges: incomplete and incorrect.
• In one-line explaination, it runs over a CSV ffle with each line as a tick. The trading
strategy acts on the tick data and perform buy/sell operations.
• All cpp ffles are in \src
• All hpp ffles are in \include
Use Replit tools
• When you press Run button, the program shasll run in the Console. However, you need
to scroll back in history for the output.
• You could use Code Search (Shortcut: Ctrl+Shift+F) to search for text in the project.
• For manual mode, usually you don’t need to, you could open the Shell tool to type make
for compilation and then type ./main to run the program. make shall auto-detect any
recently changed ffle and recompile the program. If you want to recompile every thing,
make clean and then make.
3Aku’s class organization
• I created a simple chart to show the class organization of Aku’s simulator. You could use
it as a reference.
4

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
