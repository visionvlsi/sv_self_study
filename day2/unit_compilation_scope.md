# Unit Compilation Scope:

![image](https://user-images.githubusercontent.com/98731221/208313245-37d5ca31-4d6e-46e6-94ae-63e31e6a8770.png)

![image](https://user-images.githubusercontent.com/98731221/208313936-77277a0b-5ae1-4332-b506-a2dde5421405.png)

![image](https://user-images.githubusercontent.com/98731221/208338191-1226c975-9d05-4624-8876-f6b7f7cdb496.png)

![image](https://user-images.githubusercontent.com/98731221/208338362-e3ae497f-5bdd-468f-b979-bd20547dbdc4.png)

![image](https://user-images.githubusercontent.com/98731221/208344336-fc7a6568-bb68-47f6-b637-4b9991e1f293.png)

![image](https://user-images.githubusercontent.com/98731221/208344447-3b063b4c-1788-4cea-abbe-bedbb497de19.png)

![image](https://user-images.githubusercontent.com/98731221/208344826-3fb7f7c8-4cd8-4de4-9b81-18130044d6cb.png)

![image](https://user-images.githubusercontent.com/98731221/208345887-1e9e37fa-f4a3-45e4-9ee6-75499ae209cb.png)

![image](https://user-images.githubusercontent.com/98731221/208346832-9be92235-ee40-451b-9184-4d012d158057.png)

![image](https://user-images.githubusercontent.com/98731221/208348829-d8db56ff-5c05-471c-b30a-74b9d3cea800.png)



## Ex1: mod1.sv

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

## Ex2: mod2.sv
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
