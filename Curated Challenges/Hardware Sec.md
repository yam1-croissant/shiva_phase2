# I like logic more

## Flag: HTB{073c53212070_0n_23_d35}

## Steps - 

With the given hint that the description talks about microsd it might be a MicroSD protocol decoding (SPI mode) . Using Logic 2 we see 4 channels -

<img width="1753" height="853" alt="image" src="https://github.com/user-attachments/assets/df5beaea-0425-46e3-9e92-abfa3aac0e60" />

<img width="1882" height="858" alt="f8bfd75c-8b5c-49ca-906d-69beca0d96d9" src="https://github.com/user-attachments/assets/10f0c31c-94cf-4691-bd60-aabd60809add" />

In SPI communication their 4 channels are MOSI, MISO, CS and CLK. They have their own unique waveforms

CLK - usually goes from 0-1-0-1-0-1 and flips rapidly ,so D3 channel matches it

CS - is usually high most of the time and then low when a command is being sent so that would be D2 Channel [ dont be fooled, scroll more to the side you'll see its mostly high]

MOSI - it changes during clock pulses when CS is low so , D1 Channel


MISO - shows bursts of data AFTER the MOSI command so , D0 Channel

After understanding and choosing the right channels, with the help of SPI (spy) analyzer we get this

<img width="1860" height="938" alt="image" src="https://github.com/user-attachments/assets/e86ce39b-d5e3-4d68-a416-b7f959bbc242" />

After that by changing to ascii, and scrolling through a whole lot of data 

<img width="475" height="758" alt="image" src="https://github.com/user-attachments/assets/fdf53e74-f8fa-40ec-b6a5-9f3825c21083" />
```
name	start_time	duration	mosi	miso
SPI	2.49367222	0.0000019	ÿ	H
SPI	2.49367584	0.0000019	ÿ	T
SPI	2.49367946	0.00000192	B
SPI	2.4936831	0.0000019	ÿ	  {
SPI	2.49368672	0.00000192	u
SPI	2.49369036	0.0000019	ÿ	n
SPI	2.49369398	0.00000192	p
SPI	2.49369762	0.0000019	ÿ	2
SPI	2.49370124	0.0000019	ÿ	0
SPI	2.49370488	0.0000019	ÿ	7
SPI	2.4937085	0.0000019	ÿ	  3
SPI	2.49371212	0.00000192	c
SPI	2.49371576	0.0000019	ÿ	7
SPI	2.49371938	0.00000192	3
SPI	2.49372302	0.0000019	ÿ	d
SPI	2.49372664	0.0000019	ÿ	_
SPI	2.49373028	0.0000019	ÿ	5
SPI	2.4937339	0.0000019	ÿ	  3
SPI	2.49373754	0.0000019	ÿ	2
SPI	2.49374116	0.0000019	ÿ	1
SPI	2.49374478	0.00000192	4
SPI	2.49374842	0.0000019	ÿ	1
SPI	2.49375204	0.00000192	_
SPI	2.49375568	0.0000019	ÿ	p
SPI	2.4937593	0.0000019	ÿ	  2
SPI	2.49376294	0.0000019	ÿ	0
SPI	2.49376656	0.0000019	ÿ	7
SPI	2.49377018	0.00000192	0
SPI	2.49377382	0.0000019	ÿ	c
SPI	2.49377744	0.00000192	0
SPI	2.49378108	0.0000019	ÿ	1
SPI	2.4937847	0.00000192	ÿ	5
SPI	2.49378834	0.0000019	ÿ	_
SPI	2.49379196	0.0000019	ÿ	0
SPI	2.4937956	0.0000019	ÿ	  n
SPI	2.49379922	0.0000019	ÿ	_
SPI	2.49380284	0.00000192	5
SPI	2.49380648	0.0000019	ÿ	3
SPI	2.4938101	0.00000192	ÿ	c
SPI	2.49381374	0.0000019	ÿ	u
SPI	2.49381736	0.0000019	ÿ	2
SPI	2.493821	0.0000019	ÿ	  3
SPI	2.49382462	0.0000019	ÿ	_
SPI	2.49382826	0.0000019	ÿ	d
SPI	2.49383188	0.0000019	ÿ	3
SPI	2.4938355	0.00000192	ÿ	v
SPI	2.49383914	0.0000019	ÿ	1
SPI	2.49384276	0.00000192	c
SPI	2.4938464	0.0000019	ÿ	  3
SPI	2.49385002	0.0000019	ÿ	5
SPI	2.49385366	0.0000019	ÿ	}
SPI	2.49385728	0.0000019	ÿ	\r
SPI	2.4938609	0.00000192	ÿ	\n
```
```
HTB{073c53212070_0n_23_d35}
```


# Red Devil

# Formware 

# Speed thrills but kills

# Gates of Mayhem
