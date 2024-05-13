# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

APPARATUS REQUIRED:

Vivado 2023.1

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)


T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)



D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)



# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.
# D-FLIP FLOP
VERILOG CODE
~~~
module Dflipflop(D,clk,reset,Q);
input D;
input clk;
input reset;
output reg Q;
always @(posedge clk)
begin
 if(reset==1'b1)
  Q <= 1'b0;
 else
  Q <= D;
end
endmodule
~~~

OUTPUT:

<img width="962" alt="d_flipfop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/f57d74d6-3e76-41dc-84be-860904351e48">
<img width="962" alt="verilog d flip" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/a234cf46-c2ab-49a3-9d76-c4ba2f106838">


# JK FLIP FLOP

VERILOG CODE:
~~~
module JK_flipflop (q, q_bar, j,k, clk,reset);
input j,k,clk, reset;
output reg q;
output q_bar;
always@(posedge clk)
begin
  if(!reset)        
    q <= 0;
  else 
  begin
      case({j,k})
        2'b00: q <= q;    // No change
        2'b01: q <= 1'b0; // reset
        2'b10: q <= 1'b1; // set
        2'b11: q <= ~q; // Toggle
      endcase
  end
end
assign q_bar = ~q;
endmodule
~~~

OUTPUT:
<img width="962" alt="jk flipfop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/1d531d02-4af8-4f5a-89f2-3fd7156cbcb7">
<img width="962" alt="verriolg jk flipfop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/c080f42f-e595-43c3-809f-002896ad0846">


# MOD-10 COUNTER

VERILOG CODE:
~~~
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
~~~

OUTPUT:

<img width="962" alt="mod 10 counter" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/c3de4345-cc63-4ad7-84be-a34824a50b9c">
<img width="962" alt="verilog mod 10" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/6b7cde7f-a59a-4af1-8687-4fb414d9bf3f">


# RIPPLE CARRY COUNTER

VERILOG CODE:
~~~
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule
module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule
module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf0(q[0],clk,rst);
tff tf1(q[1],q[0],rst);
tff tf2(q[2],q[1],rst);
tff tf3(q[3],q[2],rst);
endmodule
~~~

OUTPUT:

<img width="962" alt="ripple carry counter" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/bacae57e-902c-4441-9885-d0712388dfa0">
<img width="962" alt="verilog carry counter" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/3d4038ce-6610-40e2-a084-efa65d08e43e">


# SR FLIP FLOP

VERILOG CODE:
~~~
module sr_flipflop(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
~~~

OUTPUT:

<img width="962" alt="sr flipfop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/e27f7186-3a2a-41ae-a34d-ffeceba454a0">
<img width="962" alt="verilog sr flipfop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/d9ac4afa-6a0b-4fdb-8480-b38117172d39">


# T FLIP FLOP

VERILOG CODE:
~~~
module T_flipflop(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
~~~

OUTPUT:

<img width="962" alt="t flip flop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/8ff417da-2a48-43d1-b365-47d4b9c6e6b2">
<img width="962" alt="verilog t flipfop" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/47885c7a-6132-4438-8f20-3113b429a26d">


# UP-DOWN COUNTER

VERILOG CODE:
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

OUTPUT:

<img width="617" alt="up down counter" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/930238e6-ac1f-4f0d-a872-7df3ab5ecbe2">
<img width="962" alt="verilog up down" src="https://github.com/yuva007tech/VLSI-LAB-EXP-4/assets/123287599/ac0de8ec-c9a9-4c95-bdd9-e5960ed4c0d7">


RESULT:
Hence The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.
