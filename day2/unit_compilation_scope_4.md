# Unit compilation another example 

## File reg_pkg.sv

```
package reg_pkg;

parameter VERSION ="1.2a";

reg resetN = 1;

typedef struct packed{

reg [31:0] address;
reg [31:0] data;
reg [7:0]opcode;

}instruction_word_t;

function automatic int log2(input int n);

	if(n<=1) return(1);
	log2 = 0;
	while (n > 1) begin
	
		n = n/2;
		log2++;
	end
	return(log2);
endfunction

endpackage
```
## File register.sv
```
import reg_pkg::*;

module register(output instruction_word_t q,
				input instruction_word_t d,
				input wire clock);
				
				
				always@(posedge clock, negedge resetN)
					if(!resetN) q<=0;
					else q<=d;
endmodule
```

## File p1.sv
```
import reg_pkg::*;
module top;

instruction_word_t out,in;
bit clock;

register i1(out,in,clock);

always #5 clock=~clock;

initial begin

$display("\n Version is %s (expect 1.2a)\n", VERSION);
$display("\n log2 of 4096 is %0d (expect 12)\n", log2(4096));

in={32'h10,32'h20,8'h5};
#1 resetN=0;

@(posedge clock) resetN<=1;
repeat(2) @(negedge clock);
$display("\n in.data=%0d out.data=%0d is  (expect 32,32)\n", in.data,out.data);
@(negedge clock) $finish;
end
endmodule
	
```
