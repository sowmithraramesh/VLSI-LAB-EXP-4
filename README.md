
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

## AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

## APPARATUS REQUIRED:
Xilinx 14.7
Spartan6 FPGA

## PROCEDURE:
##### STEP:1  Start  the Xilinx navigator, Select and Name the New project.
##### STEP:2  Select the device family, device, package and speed.       
##### STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
##### STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
##### STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
##### STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
##### STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
##### STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
##### STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
##### STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
##### STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

## SR FLIPFLOP

#### LOGIC DIAGRAM

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


#### VERILOG CODE
```
module sr_ff(clk,q,rst,s,r);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=1'b0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=1'b0;
2'b10:q=1'b1;
2'b11:q=1'bx;
endcase
end
end
endmodule
```
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/c77fe42b-ec9d-4f69-b0a7-9c8d9fac8492)

## JK FLIPFLOP

#### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

#### VERILOG CODE
```
module jk_ff(clk,q,rst,j,k);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=1'b0;
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
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/a9456174-e11e-4ae1-b5bc-97bf3de670c3)

## T FLIPFLOP

#### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

#### VERILOG CODE
```
module t_ff(clk,q,rst,t);
input t,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=1'b0;
else
if(t==0)
q=q;
else
q=~q;
end
endmodule
```
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/cf8e1b84-d343-4d78-ae41-fce30929d60a)

## D FLIPFLOP

#### LOGIC DIAGRAM
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

#### VERILOG CODE
```
module d_ff(clk,q,rst,d);
input d,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/bc379b5d-868f-4b8b-a1e1-ea760a37f68c)

## MOD 10 COUNTER

#### LOGIC DIAGRAM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/77bdf061-1f68-411d-a1da-0d1e5dcbc3eb)

#### VERILOG CODE
```
module mod_10(clk,rst,out);
input clk,rst;
output reg[3:0]out;
always@(posedge clk)
begin
if(rst==1|out==9)
out=4'b0;
else
out=out+1;
end
endmodule
```
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/2cdf576a-0aed-435f-bafc-8a74b5f08c55)

## UPDOWN COUNTER

#### LOGIC DIAGRAM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/58a1106e-b2e7-4b0c-8911-01b22af59ba6)

#### VERILOG CODE
```
module updowncounter(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always @(posedge clk)
begin
if(rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/16686f0b-de0d-4422-b27d-94967ed9ac6e)

## RIPPLE CARRY COUNTER
![Screenshot 2024-05-17 122740](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/7e819821-ff00-41d9-b2a1-4c78d81bc580)

#### VERILOG CODE
```
module ripplecounter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tff0(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q);
endmodule
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset
or negedge clk)
if(reset)
q = 1'b0;
else
q = d; 
endmodule
```
#### OUTPUT WAVEFORM
![image](https://github.com/sowmithraramesh/VLSI-LAB-EXP-4/assets/166893766/c401e357-4787-4e42-a82f-03141de526c6)


## RESULT:
 The simulation and synthesis of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE are successfully verified.






