# Sequence-Detector
# NAME : MOHAMMED SHAHITH S
# REG NO: 212223060162

## 1.Aim

To design and simulate a sequence detector using both Moore and Mealy state machine models in Verilog HDL, and verify their functionality through a testbench using the Vivado 2023.1 simulation environment. The objective is to detect a specific sequence of bits (e.g., 1011) and compare the Moore and Mealy designs.

## 2.Apparatus Required:

Vivado 2023.1 or equivalent Verilog simulation tool.
Computer system with a suitable operating system.

## 3.Procedure:

Launch Vivado 2023.1:
Open Vivado and create a new project.

## 4.Write the Verilog Code for Sequence Detector (Moore and Mealy FSM):

## Design two Verilog modules:

one for a Moore FSM and another for a Mealy FSM to detect a sequence such as 1011.

## Create the Testbench:

Write a testbench to apply input sequences and verify the output of both FSM designs.

## Add the Verilog Files:

Add the Verilog code for both FSMs and the testbench to the Vivado project.

## Run Simulation:

Run the simulation and observe the output to check if the sequence is detected correctly.

## Observe the Waveforms:

Analyze the waveform to ensure both the Moore and Mealy machines detect the sequence as expected.

## Save and Document Results:

Capture the waveforms and include the results in the final report.

## PROGRAM:
```
module moore_sequence_detector (
    	input clk,
    	input reset,
    	input seq_in, 
	output reg detected );
parameter  [2:0] S0=2'b000,
                 S1=2'b001,
                 S2=2'b010,
                 S3=2'b011,
                 S4=2'b100;

reg [2:0]  current_state, next_state;

// State transition logic
    always @(posedge clk or posedge reset) begin
        if (reset)
        begin
            current_state <= S0;
            detected = 0;
        end
        else
            current_state <= next_state;
    end
    // Next state and output logic
    always @(*) begin
          // Default: no detection
        case (current_state)
            S0: begin
                if (seq_in)
                    next_state = S1;
                else
                    next_state = S0;
            end
S1: 
	begin
                	if (seq_in)
                   	 	next_state = S1;
                	else
                    		next_state = S2;
           	 end
            S2: begin
                if (seq_in)
                    next_state = S1;
                else
                    next_state = S3;
            end
S3: begin
                if (seq_in) begin
                    next_state = S4;
                    detected = 1;  // Sequence 1001 detected
                end else
                    next_state = S0;
            end
            S4: begin
                next_state = S0;  // Return to the start after detection
            end
            default: next_state = S0;
        endcase
    end
endmodule
```
## OUTPUT:
![Screenshot 2025-05-17 144643](https://github.com/user-attachments/assets/7a46ed2f-850e-4d99-8761-ef031c4b5f75)



## Conclusion:
In this experiment, Moore and Mealy FSMs were successfully designed and simulated to detect the sequence 1011. Both designs worked as expected, with the main difference being that the Moore FSM generated the output based on the current state, while the Mealy FSM generated the output based on both the current state and input. The testbench verified the functionality of both FSMs, demonstrating that the Verilog HDL can effectively model both types of state machines for sequence detection tasks.
