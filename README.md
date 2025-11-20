# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```verilog
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @ (posedge clk) 
begin
if (rst==1)
q <= 0;
else if(s==0 && r==0)
q <= q;
else if(s==0 && r==1)
q <= 1'b0;
else if(s==1 && r==0)
q <= 1'b1;
else
q <= 1'bx;
end
endmodule

```
### SR Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module srff_tb;
reg s,r,clk,rst;
wire q;
srff uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial begin
clk=0;s=0;r=0;rst=1;
#10; 
rst=0;
#10; s=1; r=0; 
#10; s=0; r=0; 
#10; s=0; r=1; 
#10; s=1; r=1;
#10; s=1; r=0; 
#20;
$finish;
end
endmodule



```
#### SIMULATION OUTPUT

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/014d6217-3e22-42a6-bd3e-d0120f4ac309" />


### JK Flip-Flop (Non Blocking)
```verilog
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk) 
begin
if (rst==1)
q <= 0;
else if(j==0 && k==0)
q <= q;
else if(j==0 && k==1)
q <= 1'b0;
else if(j==1 && k==0)
q <= 1'b1;
else
q <= ~q;
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module jkff_tb;
reg j,k,clk,rst;
wire q;
jkff uut(j,k,clk,rst,q);
always #5 clk = ~clk;
initial begin
clk = 0;
j = 0; k = 0;
rst = 1;
#10 rst = 0;
#10 j = 1; k = 0; 
#10 j = 0; k = 0; 
#10 j = 0; k = 1; 
#10 j = 1; k = 1; 
#10 j = 1; k = 0; 
#20 $finish;
end
endmodule



```
#### SIMULATION OUTPUT

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/8e63c1ea-91c8-4305-9928-0c423b612085" />


### D Flip-Flop (Non Blocking)
```verilog
module d_ff(D,clk,rst,Q);
input D,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q<=0;
else
    Q<=D;
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
`timescale 1ns / 1ps
module d_ff_tb;
reg D,rst,clk;
wire Q;
d_ff uut(D,clk,rst,Q);
always #5 clk= ~clk;
initial
begin
D=0;clk=0;rst=1;#10;
rst=0;D=0;#10;
D=1;#20;
$finish;
end
endmodule

```

#### SIMULATION OUTPUT

<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/7cdc1e6f-da7e-46c8-b0ad-c273160b180f" />


### T Flip-Flop (Non Blocking)
```verilog
module t_ff(T,clk,rst,Q);
input T,clk,rst;
output reg Q;
always @(posedge clk)
begin
if (rst==1)
    Q <= 0;
else if (T==0)
    Q <= Q;
else
    Q <= ~Q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog

module t_ff_tb;
reg T,rst,clk;
wire Q;
t_ff uut(T,clk,rst,Q);
always #5 clk = ~clk;
initial
begin
T=0; clk=0; rst=1; #10;
rst=0; #10;
T=0;#10;
T=1; #10;
$finish;
end
endmodule




```

#### SIMULATION OUTPUT

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/4d8103a6-4f8a-4a14-8329-4c9043c4d956" />


### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
