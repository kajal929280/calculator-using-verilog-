# calculator-using-verilog-
module Calculator (
    input [3:0] A,       // First operand
    input [3:0] B,       // Second operand
    input [1:0] op_code, // Operation code
    output reg [7:0] result // Output result
);

always @(*) begin
    case(op_code)
        2'b00: result = A + B; // Addition
        2'b01: result = A - B; // Subtraction
        2'b10: result = A * B; // Multiplication
        2'b11: result = (B != 0) ? (A / B) : 8'b00000000; // Division (check for zero)
        default: result = 8'b00000000; // Default case
    endcase
end

endmodule





//testbench
`timescale 1ns / 1ps

module Calculator_tb;

    reg [3:0] A, B;
    reg [1:0] op_code;
    wire [7:0] result;

    Calculator uut (
        .A(A),
        .B(B),
        .op_code(op_code),
        .result(result)
    );

    initial begin
        $monitor("A=%d, B=%d, op_code=%b, result=%d", A, B, op_code, result);

        A = 4'd5; B = 4'd3; op_code = 2'b00; #10; // Addition (5+3)
        A = 4'd7; B = 4'd2; op_code = 2'b01; #10; // Subtraction (7-2)
        A = 4'd3; B = 4'd4; op_code = 2'b10; #10; // Multiplication (3*4)
        A = 4'd8; B = 4'd2; op_code = 2'b11; #10; // Division (8/2)
        A = 4'd6; B = 4'd0; op_code = 2'b11; #10; // Division by zero

        $stop;
    end
endmodule

