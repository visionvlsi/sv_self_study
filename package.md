# About SystemVerilog packages 

1. How to refer to package contents

![image](https://user-images.githubusercontent.com/98731221/208306102-d295e4ab-8db2-4843-83f4-77eeddfa8dba.png)


Ex1:

	<code>
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
	</code>
