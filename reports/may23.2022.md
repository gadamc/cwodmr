# Introduction

# G. Adam Cox

* 2008
  * Ph.D. @ UW - neutrino physics (Sudbury Neutrion Observatory)
* 2008-2013
  * postdocs - dark matter detection (EDELWEISS - France/Germany)
  * teaching
* 2013 - industry (Seattle)
  * data science
* Summer 2022 -- Sabbatical

<br><br><br>
<br><br><br>

# Primary Goal
#### General Purpose Community Microscope
#### Easily Maintainable

<br><br>

### Near Term Goals
* CW ODMR
* Pulsed ODMR
* Rabi
* Hahn-Echo


<br><br><br>
<br><br><br>



# Qudi Software

* Developed by Inst. for Quantum Optics @ Ulm University
* General Purpose to support many different hardware
* Configuration Files to define specific setup
* Extensible
* Python
* GUI



<br><br><br>
<br><br><br>

# CW ODMR with Qudi

![Qudi CW ODMR](images/may23.2022/qudi-cw-odmr.jpg)


<br><br><br>
<br><br><br>

# CW DIY

[Jupyter Notebook Code](../cwodmr/my_cw_odmr_v1.ipynb)

![DIY CW ODMR](images/may23.2022/diy-cw-odmr.png)




<br><br><br>
<br><br><br>

# No Clock

* No clock to synchronize hardware

### Demonstration

#### 0.20 seconds

```python
clock_task, data_task, data_reader = configure_tasks()

rf_generator._write('g1')    #starts MW scan from beginning
time.sleep(0.20) # add artificial delay -- expect to shift location of MR frequency in the data

clock_task.start()
data_task.start()

read_samples = data_reader.read_many_sample_double(data_buffer, number_of_samples_per_channel=n_steps, timeout=read_write_timeout)

```

![DIY CW ODMR - delay of 0.20 seconds between start of scan and data acquisition](images/may23.2022/diy-cw-odmr-delta_t_0.20.png)

#### 0.30 seconds

```python
time.sleep(0.30) # add artificial delay -- expect to shift location of MR frequency in the data
```

![DIY CW ODMR - delay of 0.30 seconds between start of scan and data acquisition](images/may23.2022/diy-cw-odmr-delta_t_0.30.png)


#### 0.40 seconds

```python
time.sleep(0.40) # add artificial delay -- expect to shift location of MR frequency in the data
```

![DIY CW ODMR - delay of 0.40 seconds between start of scan and data acquisition](images/may23.2022/diy-cw-odmr-delta_t_0.40.png)


#### 0.50 seconds

```python
time.sleep(0.50) # add artificial delay -- expect to shift location of MR frequency in the data
```

![DIY CW ODMR - delay of 0.50 seconds between start of scan and data acquisition](images/may23.2022/diy-cw-odmr-delta_t_0.50.png)




* Adding hardware clock / trigger is immediate next step.
  * trigger start of RF scan to synchronize with start of acquisition
  * more reading of NI/Windfreak documentation





<br><br><br>
<br><br><br>


# Qudi v. DIY

What's the best route to take?

* DIY software should be relatively simple
  * based on `nidaqmx`
* Can use various visualization tools available in python with simple code base
* Qudi code organization / design patterns
  * feels difficult to extend (GUI code and logic/hardware code not separated enough)
  * may be more difficult for future QT3 students/users to maintain
* Qudi documentation is not fully developed
* main developer (former PhD student) has now moved on
  * uncertain future
* to use Qudi, we would **still** need to write software for our hardware that fits into Qudi


Uncertain which direction to recommend, but in the near-term, DIY won't be a wasted effort
because would need to write that software anyways to go into Qudi.

Perhaps Qudi will make more since after DIY attempt.
