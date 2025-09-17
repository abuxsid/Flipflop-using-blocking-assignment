# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

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

### SR Flip-Flop (Blocking)
```verilog
module SR_ff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @(posedge clk)
begin
if(rst)
begin
q=1'b0;
end
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=1'b0;
2'b10:q=1'b1;
2'b11:q=1'bx;
default q=1'bz;
endcase
end
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
module SR_ff_tb;
reg clk_t,rst_t,s_t,r_t;
wire q_t;
SR_ff dut(.clk(clk_t),.rst(rst_t),.r(r_t),.s(s_t),.q(q_t));
initial
begin
clk_t=1'b0;
rst_t=1'b1;
#20
rst_t=1'b0;
s_t=1'b0;
r_t=1'b0;
#20
s_t=1'b0;
r_t=1'b1;
#20
s_t=1'b1;
r_t=1'b0;
#20
s_t=1'b1;
r_t=1'b1;
end
always #10 clk_t=~clk_t;
endmodule


```
#### SIMULATION OUTPUT
<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/98cb6020-7d30-4552-8fe2-e9b05e825228" />

---

### JK Flip-Flop (Blocking)
```verilog
module JK_ff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @(posedge clk)
begin
if(rst)
begin
q=1'b0;
end
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=1'b0;
2'b10:q=1'b1;
2'b11:q=~q;
endcase
end
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog
module jk_ff_tb;
reg clk_t,rst_t,j_t,k_t;
wire q_t;
JK_ff dut(.clk(clk_t),.rst(rst_t),.j(j_t),.k(k_t),.q(q_t));
initial
begin
clk_t=1'b0;
rst_t=1'b1;
#120
rst_t=1'b0;
j_t=1'b0;
k_t=1'b0;
#120
j_t=1'b0;
k_t=1'b1;
#120
j_t=1'b1;
k_t=1'b0;
#120
j_t=1'b1;
k_t=1'b1;
end
always #10 clk_t=~clk_t;
endmodule


```
#### SIMULATION OUTPUT
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/78e867fd-cdd1-425b-9d6a-1dad8498b09d" />

---
### D Flip-Flop (Blocking)
```verilog
module d_ff(clk,rst,din,dout);
input clk,rst,din;
output reg dout;
always @(posedge clk)
begin
if(rst)
begin
dout=0;
end
else
begin
dout=din;
end
end
endmodule
```
### D Flip-Flop Test bench 
```verilog
module d_ff_tb;
reg clk_t,rst_t,din_t;
wire dout_t;
d_ff dut(.clk(clk_t),.rst(rst_t),.din(din_t),.dout(dout_t));
initial
begin
clk_t=1'b0;
rst_t=1'b1;
#120
rst_t=1'b0;
din_t=1'b0;
#120
din_t=1'b1;
end
always #10 clk_t=~clk_t;
endmodule


```

#### SIMULATION OUTPUT

<img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/4fd7abd3-eb74-47c5-b6ad-a29a4fc63f35" />


---
### T Flip-Flop (Blocking)
```verilog
module t_ff(clk,rst,tin,tout);
input clk,rst,tin;
output reg tout;
always @(posedge clk)
begin
if(rst)
begin
tout=1'b0;
end
else if(tin)
begin
tout=~tout;
end
else
begin
tout=tout;
end
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
module t_ff_tb;
reg clk_t,rst_t,tin_t;
wire tout_t;
t_ff dut(.clk(clk_t),.rst(rst_t),.tin(tin_t),.tout(tout_t));
initial
begin
clk_t=1'b0;
rst_t=1'b1;
#120
rst_t=1'b0;
tin_t=1'b0;
#120
tin_t=1'b1;
end
always #10 clk_t=~clk_t;
endmodule


```

#### SIMULATION OUTPUT

<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/8bf747d5-bbbf-4128-94f2-d20d4a264a88" />



---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
