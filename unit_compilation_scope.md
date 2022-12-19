# Unit Compilation Scope:

![image](https://user-images.githubusercontent.com/98731221/208313245-37d5ca31-4d6e-46e6-94ae-63e31e6a8770.png)

![image](https://user-images.githubusercontent.com/98731221/208313936-77277a0b-5ae1-4332-b506-a2dde5421405.png)


## Ex1:

```
function void print;
$display($time, "::comp1");
endfunction

module mod1;

	function void print;
	$display("%t::mod1",$time);
	endfunction
	
	
 initial 
 begin
 $unit::print(); //prinys comp1
 print(); //prints mod1
 end
 
 endmodule
```

Ex2:
```
function void print;
	$display($time, "::comp2");
endfunction

module mod2;

	mod3 mod1();
	
	function void print;
		$display("%t::mod2",$time);
	endfunction
	
	initial
	begin
		$root.mod1.print();
		mod1.print();
		$unit::print();
	end
endmodule

module mod3;
	function void print;
	$display("%t::mod3",$time);
	endfunction
endmodule
```