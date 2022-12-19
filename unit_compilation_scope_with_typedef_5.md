# Unit compilation with type definition

#### file definitions.sv
```
`ifndef DEFS_DONE
`define DEFS_DONE

package definitions;

	parameter VERSION="1.1";
	
	typedef enum{ADD, SUB,MUL} opcodes_t;
	
	typedef struct
	{
	logic [31:0]a,b;
	opcodes_t opcode;
	}instruction_t;
	
	function automatic[31:0]multiplier(input [31:0]a,b);
	
	return a*b;
	
	endfunction
	
	endpackage
	
import definitions::*;

`endif

```
#### file pkg_in_unit.sv

```
`include "definitions.sv"

module top;

instruction_t test_word;
logic [31:0] alu_out;
logic clock=0;
ALU dut(.IW(test_word), .result(alu_out), .clock(clock));
always #10 clock=~clock;
initial begin
	@(negedge clock)
	test_word.a=5;
	test_word.b=7;
	test_word.opcode=ADD;
	@(negedge clock)
	$display("alu_out=%0d(expected 12)",alu_out);
	$finish;
	end
	endmodule
```

#### file ALU.sv

```
`include "definitions.sv"


module ALU

(input instruction_t IW,
input logic clock,
output logic [31:0]result
);

always_comb

begin

case(IW.opcode)

ADD:result= IW.a + IW.b;

SUB:result = IW.a - IW.b;

MUL:result = definitions::multiplier(IW.a, IW.b);

endcase

end

endmodule
```

#### To compile vlog +define+definitions .\definitions.sv .\ALU.sv .\pkg_in_unit.sv
