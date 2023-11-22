# Vacant Parking Slot Detector

<!-- First Section -->
## Team Details
<details>
  <summary>Detail</summary>

  > Semester: 3rd Sem B. Tech. CSE

  > Section: S1
		
  > Member-1: Adarsh Ranjan, 221CS103, adarshranjan.221cs103@nitk.edu.in

  > member-2: Rian Shane Pinto, 221CS144, rian.221cs144@nitk.edu.in	

  > Member-3: 	Siddharth Gupta	, 221CS153, siddharthgupta.221cs153@nitk.edu.in
</details>

<!-- Second Section -->
## Abstract
<details>
  <summary>Detail</summary>

### Introduction:
  To accomplish faster, easier, and denser parking of automobiles during the majority of the time they remain inactive, smart parking combines technology and human ingenuity. 
This method aims to utilize as few resources as possible, such as fuel, time, and space.

To reduce urban congestion, mitigate environmental impact, and improve overall urban mobility, a better parking solution is necessary. This solution addresses the increasing issue of limited parking spaces, optimizing their usage and reducing the amount of time spent searching for a parking space. This not only reduces traffic congestion but also reduces carbon emissions, thus contributing to a more environmentally friendly environment. 

Furthermore, improved parking solutions may also contribute to economic growth by increasing the accessibility of businesses, thus enhancing the quality of life within cities and promoting sustainable urban development.

### Our Contribution:

Our team aims to create a prototype that is designed to reduce human intervention in searching for parking spots. Thus, creating a more efficient, accurate, and potentially cost-effective solution.
The project streamlines the parking process, making it more convenient for drivers.

The project features a counter, to keep track of the vacant spots in the parking space. This creates a quicker flow of traffic in such parking spaces.

Moreover, the position of the nearest available parking space is also displayed to the user at the entrance of the parking spot. This reduces the dependency on humans.


</details>

<!-- Third Section -->
## Working
<details>
  <summary>Detail</summary>
Our team aims to create a prototype that is designed to reduce human intervention in searching for parking spots. Thus, creating a more efficient, accurate, and potentially cost-effective solution.
The project streamlines the parking process, making it more convenient for drivers.

The project features a counter, to keep track of the vacant spots in the parking space. This creates a quicker flow of traffic in such parking spaces.

Moreover, the position of the nearest available parking space is also displayed to the user at the entrance of the parking spot. This reduces the dependency on humans.
User Input: The user approaches the Vacant Parking Slot Detecting Machine and inputs their vehicle type through a keypad, representing it as a password (e.g., "truck" for a truck, "bus" for a bus, "4wheeler" for a 4-wheeler, or "2wheeler" for a 2-wheeler).

Password Verification: The system checks the entered password against the predefined vehicle types. If the password is valid, access is granted. If the password is incorrect, the system counts the number of incorrect attempts.

Access Granted: Upon successful verification, the system uses the decoder to determine the nearest available parking spot for the user's vehicle type based on the output of the priority encoders.

Parking Slot Indication: The system guides the user to the designated parking spot through LED indicators or display panels.

Access Denied: If a user exceeds three incorrect attempts, the system denies access and alerts the user.

### Flow of Simulation:
![image](https://github.com/RianPinto/Vacant-Parking-Slot-Detector/assets/139946131/ed260b44-41ba-439d-8f93-a2369e9fd7d7)


### Functionality
Encoder:	Four priority encoders are utilized to detect the availability of parking slots for each vehicle type: truck, bus, 4-wheeler, and 2-wheeler. These priority encoders receive input signals from various parking spots and prioritize them based on vehicle type. The output of each priority encoder represents the availability status of parking spots for that specific vehicle type.

Counter	Counter: created using T-flipflops is used to measure 
the number of times the password has been inputted. When the count crosses three and no correct inputs have been made previously, then the circuit breaks down due to excessive failed attempts. A red LED is displayed to show an error

Decoder:	A decoder is used in the password application. When the vehicle enters its vehicle code, it is translated into one of four valid vehicles, if its password matches the given password. This translation of password to vehicle is done using a decoder
General circuits created using min terms 	1.	In the odd case when all parking slots are full, the signal is required to be sent at the parking entry, using a red led, indicating that the parking is full;
2.	To convert the result of all encoders into a suitable parking spot with respect to the vehicle code inputted

</details>

<!-- Fourth Section -->
## Logisim Circuit Diagram
<details>
  <summary>Detail</summary>
  
  > 
Sample Encoder (1/4)
> ![Singular Priority Encoder](https://github.com/RianPinto/Vacant-Parking-Slot-Detector/assets/139946131/b861c55e-2d94-4aa1-a187-e9f0792b3f01)


Password Input Segment:

![Password Input Module](https://github.com/RianPinto/Vacant-Parking-Slot-Detector/assets/139946131/a719966f-f664-423f-942d-93fa991a085b)


Password Input Along with Counter Check to Limit Password Trials:

![Password Count Check](https://github.com/RianPinto/Vacant-Parking-Slot-Detector/assets/139946131/df6aa258-636c-4401-ae24-cb83984ec030)



Main Priority Encoder Circuit:

![Main MultiEncoder Decoder Parking Display](https://github.com/RianPinto/Vacant-Parking-Slot-Detector/assets/139946131/41584575-ec24-4589-869a-a676b2233414)



</details>

<!-- Fifth Section -->
## Verilog Code
<details>
  <summary>Detail</summary>

  > Encoder-Decoder Verilog

```
module pe(d,o);

input [3:0] d;
output [1:0] o;

assign o[1] = !d[0] & !d[1];
assign o[0] = (!d[0]&d[1])|(!d[0]&!d[2]);



endmodule

module main(d,w,o);
input [15:0]d;
input [3:0] w;
output [3:0] o;

wire [1:0] t1;
wire [1:0] t2;
wire [1:0] t3;
wire [1:0] t4;
wire [1:0] t5;
wire [3:0] d1;
wire [3:0] d2;
wire [3:0] d3;
wire [3:0] d4;

assign d1[0] = d[0];
assign d1[1] = d[1];
assign d1[2] = d[2];
assign d1[3] = d[3];

assign d2[0] = d[4];
assign d2[1] = d[5];
assign d2[2] = d[6];
assign d2[3] = d[7];


assign d3[0] = d[8];
assign d3[1] = d[9];
assign d3[2] = d[10];
assign d3[3] = d[11];


assign d4[0] = d[12];
assign d4[1] = d[13];
assign d4[2] = d[14];
assign d4[3] = d[15];


pe s1(d1,t1);
pe s2(d2,t2);
pe s3(d3,t3);
pe s4(d4,t4);

assign o[0] = (w[3]&t4[0])|(w[2]&t3[0])|(w[1]&t2[0])|(w[0]&t1[0]);
assign o[1] = (w[3]&t4[1])|(w[2]&t3[1])|(w[1]&t2[1])|(w[0]&t1[1]);

pe s5(w,t5);
assign o[2] = (t5[0]);
assign o[3] = (t5[1]);


endmodule
```


Test Bench
```
module mp_tb;
reg [15:0]d;
reg [3:0] w;
wire [3:0] o;

main rian(d,w,o);

initial

begin
d=16'b1010011101100100;
w=4'b0001;
$display("P15 P14 P13 P12 | P11 P10 P9 P8 | P7 P6 P5 P4 | P3 P2 P1 P0 |    |BUS TRUCK 4W 2W | Nearest Appopriate Parking Spot |");
$monitor("%d   %d   %d   %d   | %d   %d   %d   %d | %d  %d  %d  %d  | %d  %d  %d  %d  |    |      %b      |                 %d              |",d[15],d[14],d[13],d[12],d[11],d[10],d[9],d[8],d[7],d[6],d[5],d[4],d[3],d[2],d[1],d[0],w,o);
#10;
repeat(3)
begin

w=w*2;
#10;
end


end
endmodule
```
Verilog for Password Checker and  Entry and Exit
```
module four_wheeler_module(input buzzer, 				
						input entry,			
						input exit,				
						input [3:0]password,			
						input clear,			
						input clear_new,		
						output reg gate_open,	
						output reg gate_closed,	
						output reg [1:0]count_entry,		
						output reg [1:0]count_exit,			
						output reg [12:1]num_in_park_slot,	
						output reg [2:1]count_next_entry,	
						output reg [2:1]count_next_exit,	
						output reg [12:1]num_entry_next ,	
						output reg [12:1]num_exit_next,		
						output reg [2:1] count_prev_entry,	
						output reg [2:1] count_prev_exit,	
						output reg [0:3] occupied
						);
	
always @(buzzer or password or entry or exit or clear or clear_new)
	
	begin
			if(clear==1'b1)			
			begin
			count_exit=2'd0;
			count_entry=2'd0;
			occupied = 4'b0000;
			num_in_park_slot=12'd0;
			end
			
			else if(clear==1'b0)
			begin
				count_entry=count_next_entry;;
			end
			
			else if(clear==1'b0)
			begin
				count_exit=count_next_exit;
			end
			

			count_prev_entry=count_entry;
			num_entry_next=num_in_park_slot+1;
			count_prev_exit=count_exit;
			num_exit_next=num_in_park_slot-1;

		if(entry==1'b1)
		begin
			
			if(count_entry==2'd3 &&(password==4'b0001|| password==4'b0010|| password==4'b0100|| password==4'b1000) )
			begin
				count_next_entry=2'd0;
				if (password==4'b0001) occupied[0] = 1;
				if (password==4'b0010) occupied[1] = 1;
				if (password==4'b0100) occupied[2] = 1;
				if (password==4'b1000) occupied[3] = 1;
			end
			else if(count_entry==2'd3 && (password!=4'b0001|| password!=4'b0010|| password!=4'b0100|| password!=4'b1000))
				count_next_entry=2'd1;
			else
				count_next_entry=count_entry+1;
			
			
			
			if(count_entry<2'd3)
			begin
				if(buzzer==1'b1 && (password==4'b0001|| password==4'b0010|| password==4'b0100|| password==4'b1000))
				begin
					gate_open<=1'b1;
					gate_closed<=1'b0;
					num_in_park_slot=num_entry_next;
					count_entry<=2'd0;
					if (password==4'b0001) occupied[0] = 1;
					if (password==4'b0010) occupied[1] = 1;
					if (password==4'b0100) occupied[2] = 1;
					if (password==4'b1000) occupied[3] = 1;
						
				end	
				
			end
			else if(count_entry==2'd3)
				begin
					$display("\nIncorrect password for 3 times!\nYou cannot enter the parking slot.\nSORRY!!");
				
				end

			if(buzzer==1'b0 ||(password!=4'b0001|| password!=4'b0010|| password!=4'b0100|| password!=4'b1000) )
			begin
				count_entry=count_next_entry;
				gate_open=1'b0;
				gate_closed=1'b1;
				num_in_park_slot=num_in_park_slot;
				count_entry<=1'd0;
			end
		end


		if(exit==1'b1)
		begin
		
			if(count_exit==2'd3 &&(password==4'b0001|| password==4'b0010|| password==4'b0100|| password==4'b1000) )
			begin
			count_next_exit=2'd0;
			if (password==4'b0001) occupied[0] = 0;
			if (password==4'b0010) occupied[1] = 0;
			if (password==4'b0100) occupied[2] = 0;
			if (password==4'b1000) occupied[3] = 0;
			end
			else if(count_exit==2'd3 && (password!=4'b0001|| password!=4'b0010|| password!=4'b0100|| password!=4'b1000))
			count_next_exit=2'd1;
			else
			count_next_exit=count_exit+1;
			
			
			
			if(count_exit<2'd3)
			begin
				if(buzzer==1'b1 && (password==4'b0001|| password==4'b0010|| password==4'b0100|| password==4'b1000) )
				begin
					gate_open<=1'b1;
					gate_closed<=1'b0;
					num_in_park_slot=num_exit_next;
					count_exit<=2'd0;
					if (password==4'b0001) occupied[0] = 0;
					if (password==4'b0010) occupied[1] = 0;
					if (password==4'b0100) occupied[2] = 0;
					if (password==4'b1000) occupied[3] = 0;
						
				end	
				
			end
			else if(count_exit==2'd3)
				begin
					$display("\nIncorrect password for 3 times!\nYou cannot enter the parking slot.\nSORRY!!");
				
				end

		if(buzzer==1'b0 ||(password!=4'b0001|| password!=4'b0010|| password!=4'b0100|| password!=4'b1000) )
			begin
				count_exit=count_next_exit;
				gate_open=1'b0;
				gate_closed=1'b1;
				num_in_park_slot=num_in_park_slot;
				count_exit=1'd0;
			end
		end
	end
endmodule


module four_wheeler_module_tb;
reg buzzer; 						
reg [3:0]password;								
reg clear;							
reg clear_new;						
reg entry;							
reg exit;							
wire [2:1]count_entry;				
wire [2:1]count_exit;				
wire gate_open;						
wire gate_closed;					
wire [12:1]num_in_park_slot;		
wire [2:1]count_next_entry;			
wire [2:1]count_next_exit;			
wire [12:1]num_entry_next;			
wire [12:1]num_exit_next;			
wire [2:1] count_prev_entry;		
wire [2:1] count_prev_exit;			
wire [0:3] occupied;
four_wheeler_module instance_t(buzzer,entry,exit,password,clear,clear_new,gate_open,gate_closed,count_entry,count_exit,num_in_park_slot,count_next_entry,count_next_exit,num_entry_next,num_exit_next,count_prev_entry,count_prev_exit,occupied);
initial
begin
	$dumpfile("four_wheeler_module_vcd");
	$dumpvars;
end

initial begin
	buzzer=1'b0;
	clear=1'b1;
	entry=1'b1;
	exit=1'b0;
	password=4'b0000;
	#10
		entry=1'b1;
		exit=0;
		clear=1'b0;
		buzzer=1'b1;
		password=4'b0001;
	#10
		entry=1'b1;
		exit=0;
		clear=1'b0;
		buzzer=1'b1;
		password=4'b0100;
	#10
		entry=1'b1;
		exit=0;
		clear=1'b0;
		buzzer=1'b1;
		password=4'b0011;
	#10
		entry=1'b1;
		exit=0;
		clear=1'b0;
		buzzer=1'b1;
		password=4'b1010;
	#10
		exit=1'b0;
		entry=1;
		clear=1'b0;
		buzzer=1'b1;
		password=4'b1011;
	#10
		exit=1;
		entry=0;
		buzzer=1'b1;
		password=4'b0001;
		clear=1'b0;
		
end 
initial

//$monitor("\nentry=%b\texit=%b\tBuzzer=%b\tPassword=%4b\tgate open=%b\tgate closed=%b\tnumber of vehicles in parking slot=%2d,occupied=%4b",entry,exit,buzzer,password,gate_open,gate_closed,num_in_park_slot,occupied);
$monitor("\nentry=%b\texit=%b\tBuzzer=%b\tPassword=%4b\toccupied=%4b",entry,exit,buzzer,password,occupied);
endmodule

```
</details>
<!-- Sixth Section -->

## References
<details>
  <summary>Detail</summary>

  > 
1.	https://nevonprojects.com/
2.	https://www.geeksforgeeks.org/counters-in-digital-logic/
3.	https://www.electronics-tutorials.ws/blog/7-segment-display-tutorial.html
4.	https://www.electronicsforu.com/technology-trends/learn-electronics/ldr-light-dependent-resistors-basics
5.	https://en.wikipedia.org/wiki/Parking_guidance_and_information

</details>
