# Verilog-Code-for-Swapping-Three-Numbers
## Aim
To design and simulate a Verilog HDL code for swapping the values of three numbers without using any temporary variables, and verify the correctness of the swapping operation through a testbench using the Vivado 2023.1 simulation environment.

## Apparatus Required
Vivado 2023.1 or equivalent Verilog simulation tool.

## Procedure
Launch Vivado 2023.1:

Open Vivado and create a new project.
Write the Verilog Code for Swapping:

Write the Verilog code that swaps the values of three numbers (a, b, and c) using basic arithmetic or bitwise operations without using temporary variables.
Create the Testbench:

Write a testbench to simulate the swapping operation. The testbench should initialize three numbers, trigger the swapping module, and check if the values are swapped correctly.
Add the Verilog Files:

Add the Verilog module and the testbench file to the Vivado project.
Run Simulation:

Run the behavioral simulation in Vivado to verify the swapping operation.
Observe the Waveforms:

Examine the waveform to confirm that the values of the three numbers are swapped as expected.
Save and Document Results:

Capture the waveform output and include the results in your report for verification.

## Verilog Code:
## Blocking:
```
`timescale 1ns / 1ps
module swap_three (
    input  [7:0] a_in,
    input  [7:0] b_in,
    input  [7:0] c_in,
    output [7:0] a_out,
    output [7:0] b_out,
    output [7:0] c_out
);

assign a_out = b_in;
assign b_out = c_in;
assign c_out = a_in;

endmodule

//Test Bench Blocking
`timescale 1ns / 1ps
module swap_three_tb;

    // Inputs
    reg [7:0] a_in;
    reg [7:0] b_in;
    reg [7:0] c_in;

    // Outputs
    wire [7:0] a_out;
    wire [7:0] b_out;
    wire [7:0] c_out;

    // Instantiate the Unit Under Test (UUT)
    swap_three uut (
        .a_in(a_in),
        .b_in(b_in),
        .c_in(c_in),
        .a_out(a_out),
        .b_out(b_out),
        .c_out(c_out)
    );

    initial begin
        // Display header
        $display("Time\t a_in b_in c_in => a_out b_out c_out");

        // First test case
        a_in = 8'd10;
        b_in = 8'd20;
        c_in = 8'd30;
        #10;
        $display("%0dns\t %d   %d   %d   => %d    %d    %d", 
                  $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Second test case
        a_in = 8'd5;
        b_in = 8'd15;
        c_in = 8'd25;
        #10;
        $display("%0dns\t %d   %d   %d   => %d    %d    %d", 
                  $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Third test case
        a_in = 8'd100;
        b_in = 8'd200;
        c_in = 8'd255;
        #10;
        $display("%0dns\t %d  %d  %d  => %d  %d  %d", 
                  $time, a_in, b_in, c_in, a_out, b_out, c_out);

        $finish;
    end

endmodule
 ```
## Output:
![Screenshot 2025-04-20 203827](https://github.com/user-attachments/assets/ae647d31-c3a8-4bdd-8551-6ea2c618e83c)

## Non-Blocking:

## Code:
```
`timescale 1ns / 1ps
module swap_three (
    input clk,
    input [7:0] a_in,
    input [7:0] b_in,
    input [7:0] c_in,
    output reg [7:0] a_out,
    output reg [7:0] b_out,
    output reg [7:0] c_out
);

always @(posedge clk) begin
    a_out <= b_in;
    b_out <= c_in;
    c_out <= a_in;
end

endmodule

//Testbench for non blocking
`timescale 1ns / 1ps
module swap_three_tb;

    // Inputs
    reg clk;
    reg [7:0] a_in;
    reg [7:0] b_in;
    reg [7:0] c_in;

    // Outputs
    wire [7:0] a_out;
    wire [7:0] b_out;
    wire [7:0] c_out;

    // Instantiate the Unit Under Test (UUT)
    swap_three uut (
        .clk(clk),
        .a_in(a_in),
        .b_in(b_in),
        .c_in(c_in),
        .a_out(a_out),
        .b_out(b_out),
        .c_out(c_out)
    );

    // Clock generation
    initial begin
        clk = 0;
        forever #5 clk = ~clk;  // 10ns clock period
    end

    // Test sequence
    initial begin
        // Display header
        $display("Time\t a_in b_in c_in => a_out b_out c_out");

        // Test case 1
        a_in = 8'd10;
        b_in = 8'd20;
        c_in = 8'd30;
        @(posedge clk);
        #1;
        $display("%0dns\t %3d  %3d  %3d => %3d   %3d   %3d", 
                 $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Test case 2
        a_in = 8'd5;
        b_in = 8'd15;
        c_in = 8'd25;
        @(posedge clk);
        #1;
        $display("%0dns\t %3d  %3d  %3d => %3d   %3d   %3d", 
                 $time, a_in, b_in, c_in, a_out, b_out, c_out);

        // Test case 3
        a_in = 8'd100;
        b_in = 8'd200;
        c_in = 8'd255;
        @(posedge clk);
        #1;
        $display("%0dns\t %3d  %3d  %3d => %3d   %3d   %3d", 
                 $time, a_in, b_in, c_in, a_out, b_out, c_out);

        $finish;
    end

endmodule
```
## Output:
![Screenshot 2025-04-20 204323](https://github.com/user-attachments/assets/43e214f0-e052-4227-88a3-2eda5c201b72)

## Blocking:

## Code:
```
module swap;
reg [3:0]a,b,c;
initial begin
a=4'b1000;
b=4'b0111;
c=4'b0110;

a=b;
b=c;
c=a;
end


endmodule
```
## Output:
![Screenshot 2025-04-20 204615](https://github.com/user-attachments/assets/0f407621-34c0-4312-a38d-c4cc810c2286)

## Non-Blocking:

## Code
```
module swap;
reg [3:0]a,b,c;
initial begin
a=4'b1000;
b=4'b0111;
c=4'b0110;

a<=b;
b<=c;
c<=a;
end


endmodule
```
## Output:
![Screenshot 2025-04-20 204842](https://github.com/user-attachments/assets/92054bc8-f4d7-4343-8941-33da316fe199)



## Conclusion
In this experiment, a Verilog HDL code for swapping three numbers was designed and successfully simulated. The testbench verified the swapping operation, showing that the values of three input numbers (a, b, and c) were swapped correctly without the use of temporary variables. This experiment demonstrated the effectiveness of Verilog in implementing logical operations and control mechanisms such as swapping values. The simulation results confirm the correct functionality of the design.
