---
layout: post
title: "Install Ghdl"
date: 2017-11-09 21:05:47 +0700
comments: true
categories: 
---

Kacau lah install ghdl ajah dulu buat bisa progress ta. Senggaknya biar keliatan progress.
{% highlight bash %}
sudo dnf install ghdl
{% endhighlight %}

##Coba kode vhdlnya
{%highlight bash%}
nano hello.vhdl
{%endhighlight%}

Untuk pertama coba dulu kode vhdlnya yah

{%highlight vhdl%}
--  Hello world program.
use std.textio.all; -- ngopi dari http://ghdl.readthedocs.io/en/latest/Starting_with_GHDL.html

--  Defines a design entity, without any ports.
entity hello_world is
end hello_world;

architecture behaviour of hello_world is
begin
   process
      variable l : line;
   begin
      write (l, String'("Hello world!"));
      writeline (output, l);
      wait;
   end process;
end behaviour;
{%endhighlight%}

Compile code vhdlnya dengan menggunakan ghdl

{%highlight bash%}
ghdl -a hello.vhdl
{%endhighlight%}
perintah a diatas merupakan perintah untuk menganalisa.

Membuat file excutable 
{%highlight bash%}
ghdl -e hello_world
{%endhighlight%}

{%highlight bash%}
./hello_world
{%endhighlight%}


## Membuat Full Adder

{%highlight vhdl%}
entity adder is
	port(i0, i1:in bit; ci :in bit; s:out bit; co:out bit);
end adder;

architecture rtl of adder is
begin
	s<=i0 xor i1 xor ci;
	co<=(i0 and i1) or (i0 and ci) or (i1 and ci);
end rtl;

{%endhighlight%}

Setelah membuat code adder dalam vhdl waktunya kita untuk menganalisa denga perintah seperti tadi.
{%highlight bash%}
ghdl -a adder.vhdl
{%endhighlight%}

Sayangnya adder membutuhkan testbench untuk mengetes sinyal untuk itu kita buat 
sinyal untuk dites kedalam code tersebut.

{%highlight vhdl%}


--  A testbench has no ports.
entity adder_tb is
end adder_tb;

architecture behav of adder_tb is
   --  Declaration of the component that will be instantiated.
   component adder
     port (i0, i1 : in bit; ci : in bit; s : out bit; co : out bit);
   end component;

   --  Specifies which entity is bound with the component.
   for adder_0: adder use entity work.adder;
   signal i0, i1, ci, s, co : bit;
begin
   --  Component instantiation.
   adder_0: adder port map (i0 => i0, i1 => i1, ci => ci,
                            s => s, co => co);

   --  This process does the real job.
   process
      type pattern_type is record
         --  The inputs of the adder.
         i0, i1, ci : bit;
         --  The expected outputs of the adder.
         s, co : bit;
      end record;
      --  The patterns to apply.
      type pattern_array is array (natural range <>) of pattern_type;
      constant patterns : pattern_array :=
        (('0', '0', '0', '0', '0'),
         ('0', '0', '1', '1', '0'),
         ('0', '1', '0', '1', '0'),
         ('0', '1', '1', '0', '1'),
         ('1', '0', '0', '1', '0'),
         ('1', '0', '1', '0', '1'),
         ('1', '1', '0', '0', '1'),
         ('1', '1', '1', '1', '1'));
   begin
      --  Check each pattern.
      for i in patterns'range loop
         --  Set the inputs.
         i0 <= patterns(i).i0;
         i1 <= patterns(i).i1;
         ci <= patterns(i).ci;
         --  Wait for the results.
         wait for 1 ns;
         --  Check the outputs.
         assert s = patterns(i).s
            report "bad sum value" severity error;
         assert co = patterns(i).co
            report "bad carry out value" severity error;
      end loop;
      assert false report "end of test" severity note;
      --  Wait forever; this will finish the simulation.
      wait;
   end process;
end behav;


{%endhighlight%}

Seperti bisa buat code analisa,



{%highlight bash%}
ghdl -a adder_tb.vhdl
{%endhighlight%}

buat code untuk diekseskusi

{%highlight bash%}
ghdl -e adder_tb
{%endhighlight%}

Run file test bench nya

{%highlight bash%}
ghdl -r adder_tb
{%endhighlight%}

lalu gabungkan dengan code adder dan adder_tb

{%highlight bash%}
ghdl -r adder_tb --vcd=adder.vcd
{%endhighlight%}

sekarang waktunya utnuk simulasi
{%highlight simulasi%}
gtkwave adder.vcd
{%endhighlight%}

