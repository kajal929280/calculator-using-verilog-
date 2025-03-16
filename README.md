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
