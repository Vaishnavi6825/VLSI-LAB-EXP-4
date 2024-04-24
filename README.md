# VLSI-LAB-EXP-4

SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 

To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

APPARATUS REQUIRED:

Xilinx 14.7
Spartan6 FPGA

PROCEDURE:

STEP:1  Start  the Xilinx navigator, Select and Name the New project.

STEP:2  Select the device family, device, package and speed.    

STEP:3  Select new source in the New Project and select Verilog Module as the Source type.   

STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.

STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax. 

STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table. 

STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.

STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 

STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.

STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.

STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

```
DEVELOPED BY: KIRUTHIKA M

REGISTER NUMBER: 212222060121
```


**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


VERILOG CODE:

```
module srff(s,r,clk,rst,q);
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
```

OUTPUT:

<img width="960" alt="Tff" src="https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/4d9aa873-1e43-47d8-a909-8b00194cc7b6">


**LOGIC DIAGRAM**

JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

VERILOG CODE:

```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```

OUTPUT:

![image](https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/02fd26ef-45d4-4783-ab71-1c1c89543e3c)


**LOGIC DIAGRAM**

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


VERILOG CODE:

```

module tff(clk,rst,t,q);
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

```

OUTPUT:

<img width="960" alt="Tff" src="https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/68aa1deb-d28c-4844-8bcf-04fe37c94883">


**LOGIC DIAGRAM**

D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


VERILOG CODE:

```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule

```

OUTPUT:

![image](https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/362d7845-a56a-451b-92bc-1cd289a28f28)


**LOGIC DIAGRAM**

COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

VERILOG CODE:

```
UPDOWN COUNTER:

module updown(clk,rst,updown,out);
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

```

OUTPUT:

![image](https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/dbe2582b-57c2-400e-a6ac-d18507645379)

MOD 10 COUNTER:

VERILOG CODE:

```
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
```

OUTPUT:

![image](https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/9d7e82ea-fad9-4a41-a40c-76b0ad216365)

RIPPLE COUNTER:

VERILOG CODE:

```
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
tff tf1(q[0],clk,rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule

```

OUTPUT:

![image](https://github.com/Vaishnavi6825/VLSI-LAB-EXP-4/assets/131337024/8c0c8786-9705-49c0-86ac-8d0f3cb95f2c)


RESULT

Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGNS are simulated and synthesised using Xilinx ISE.


