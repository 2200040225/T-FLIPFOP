# T-FLIPFOP

Design code:


module TFlipFlop (
    input T,      
    input clk,    
    input reset,  
    output reg Q  
);
always @(posedge clk or posedge reset)
begin
    if (reset)
        Q <= 1'b0;  
    else if (T)
        Q <= ~Q;    
end

endmodule

test bench:

module TFlipFlop_tb;
    reg T;
    reg clk;
    reg reset;
    wire Q;
    TFlipFlop uut (
        .T(T),
        .clk(clk),
        .reset(reset),
        .Q(Q)
    );
    always #5 clk = ~clk;
    initial begin
        T = 0;
        clk = 0;
        reset = 0;
        reset = 1;
        #10;
        reset = 0;
        #10 T = 1; 
        #20 T = 0;
        #20 T = 1; 
        #30 T = 1; 
        #50 $finish;
    end
    initial begin
        $monitor("Time = %0d, T = %b, clk = %b, reset = %b, Q = %b", $time, T, clk, reset, Q);
    end

endmodule
