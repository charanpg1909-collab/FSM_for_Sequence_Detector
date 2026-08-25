# FSM for Sequence Detector

# EXP NO.6.A. Sequence Detector Using Moore Machine and Mealy Machine

# Aim
To design and simulate a Finite-State-Machine-for-Sequence-Detector-1011 using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment.

# Apparatus Required
Vivado 2023.1

# Procedure
1.  Launch Vivado 2023.1 Open Vivado and create a new project.
2.  Design the Verilog Code Write the Verilog code for the RAM,ROM,FIFO Create the Testbench Write a testbench to simulate the memory behavior.
3.  The testbench should apply various and monitor the corresponding output.
4.  Create the Verilog Files Create both the design module and the testbench in the Vivado project. Run Simulation Run the behavioral simulation to verify the output.
5.  Observe the Waveforms Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
6.  Save and Document Results Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Code

# Mealy 1011
```
module mealy_1011(
    input clk,
    input rst,
    input x,
    output reg y
);

reg [1:0] state,next;

parameter S0=2'd0,
          S1=2'd1,
          S2=2'd2,
          S3=2'd3;

always @(posedge clk or posedge rst)
begin
    if(rst)
        state<=S0;
    else
        state<=next;
end

always @(*)
begin
    y=0;

    case(state)

    S0:
    begin
        if(x==1)
            next=S1;
        else
            next=S0;
    end

    S1:
    begin
        if(x==1)
            next=S1;
        else
            next=S2;
    end

    S2:
    begin
        if(x==1)
            next=S3;
        else
            next=S0;
    end

    S3:
    begin
        if(x==1)
        begin
            next=S1;
            y=1;
        end
        else
            next=S2;
    end

    default:
    begin
        next=S0;
        y=0;
    end

    endcase
end

endmodule
```

# Test bench for MEALY
```
module tb_mealy_1011;

reg clk,rst,x;
wire y;

mealy_1011 uut(
    .clk(clk),
    .rst(rst),
    .x(x),
    .y(y)
);

always #5 clk=~clk;

initial
begin
    clk=0;
    rst=1;
    x=0;

    #10 rst=0;

    x=1; #10;
    x=0; #10;
    x=1; #10;
    x=1; #10;
    x=0; #10;
    x=1; #10;
    x=1; #10;
    x=0; #10;

    #20;
    $finish;
end

endmodule
```

# Moore 1011
```
module moore_1011(
    input clk,
    input rst,
    input x,
    output reg y
);

reg [2:0] state,next;

parameter S0=3'd0,
          S1=3'd1,
          S2=3'd2,
          S3=3'd3,
          S4=3'd4;

always @(posedge clk or posedge rst)
begin
    if(rst)
        state <= S0;
    else
        state <= next;
end

always @(*)
begin
    case(state)

    S0:
    begin
        if(x==1)
            next=S1;
        else
            next=S0;
    end

    S1:
    begin
        if(x==1)
            next=S1;
        else
            next=S2;
    end

    S2:
    begin
        if(x==1)
            next=S3;
        else
            next=S0;
    end

    S3:
    begin
        if(x==1)
            next=S4;
        else
            next=S2;
    end

    S4:
    begin
        if(x==1)
            next=S1;
        else
            next=S2;
    end

    default:
        next=S0;

    endcase
end

always @(*)
begin
    if(state==S4)
        y=1;
    else
        y=0;
end

endmodule
```
# Test bench for MOORE
```
module tb_moore_1011;

reg clk,rst,x;
wire y;

moore_1011 uut(
    .clk(clk),
    .rst(rst),
    .x(x),
    .y(y)
);

always #5 clk=~clk;

initial
begin
    clk=0;
    rst=1;
    x=0;

    #10 rst=0;

    x=1; #10;
    x=0; #10;
    x=1; #10;
    x=1; #10;
    x=0; #10;
    x=1; #10;
    x=1; #10;
    x=0; #10;

    #20;
    $finish;
end

endmodule
```

# Output Waveform
MEALY MODEL
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/18bb4211-8b99-4e62-a019-57a59489f484" />

MOORE MODEL
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/75c1c51e-7eda-450b-a485-1e7f412f403b" />


# Conclusion 
The Mealy and Moore state machine for sequence 1011 was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the sequence operations and observing the output waveforms.

