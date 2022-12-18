# About SystemVerilog packages 

1. How to refer to package contents

![image](https://user-images.githubusercontent.com/98731221/208306102-d295e4ab-8db2-4843-83f4-77eeddfa8dba.png)


# Ex1:
```
	
	 package definitions;

	parameter VERSION="1.1"
	
	typedef enum{ADD, SUB,MUL} opcodes_t;
	
	typedef struct{
	logic [31:0]a,b;
	opcodes_t opcode;
	}instruction_t;
	
	function automatic[31:0]multiplier(input [31:0]a,b);
	
	return a*b;
	
	endfunction
	
	endpackage
```
# Ex2:

```
module ALU

(input definitions::instruction_t IW,
input logic clock,
output logic [31:0]result
);

always_ff@(posedge clock) begin

case(IW.opcode)

definitions::ADD:result= IW.a + IW.b;

definitions::SUB:result = IW.a - IW.b;

definitions::MUL:result = definitions::multiplier(IW.a, IW.b);

endcase

end

endmodule
```
# Ex3:

```
module ALU

(input definitions::instruction_t IW,
input logic clock,
output logic [31:0]result
);


import definitions::AND;
import definitions::SUB;
import definitions::MUL;
import definitions::multiplier;

always_ff@(posedge clock) begin

case(IW.opcode)
/*
definitions::ADD:result= IW.a + IW.b;

definitions::SUB:result = IW.a - IW.b;

definitions::MUL:result = definitions::multiplier(IW.a, IW.b);
*/

ADD:result= IW.a + IW.b;

SUB:result = IW.a - IW.b;

MUL:result = definitions::multiplier(IW.a, IW.b);
endcase

end

endmodule
```
# Ex4:
```
module ALU

(input definitions::instruction_t IW,
input logic clock,
output logic [31:0]result
);

/*
import definitions::AND;
import definitions::SUB;
import definitions::MUL;

import definitions::multiplier;
*/
import definitions::*;

always_ff@(posedge clock) begin

case(IW.opcode)
/*
definitions::ADD:result= IW.a + IW.b;

definitions::SUB:result = IW.a - IW.b;

definitions::MUL:result = definitions::multiplier(IW.a, IW.b);
*/

ADD:result= IW.a + IW.b;

SUB:result = IW.a - IW.b;

MUL:result = definitions::multiplier(IW.a, IW.b);
endcase

end

endmodule
```
# Ex5:

![image](https://user-images.githubusercontent.com/98731221/208313245-37d5ca31-4d6e-46e6-94ae-63e31e6a8770.png)

![image](https://user-images.githubusercontent.com/98731221/208313936-77277a0b-5ae1-4332-b506-a2dde5421405.png)


