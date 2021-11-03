[Tutorial's Top page](flow.md)<br>
[Previous step](register_children.md)<br>
<hr>

# Register a new bare module to ITkPD

We can register a bare-module and assemble FE chips and a seonsor tile to the registered bare-module. The way to register is following:

## 1. Start GUI

```bash
$ cd Workdir/qc-helper
$ python3 main.py
```
<br>

## 2. Choose the option to `Register Bare Module`

![choose option](../images/qc-flow/register_bare_1.png)

We log in to ITkPD.
If you don't have an account for the production DB. Please sign up following the link below:<br>
[Tutorial page for ITkPD ](https://gitlab.cern.ch/jpearkes/itkpd_tutorial/blob/master/README.md)<br>


## 3. Input bare module information

![input bare info](../images/qc-flow/register_bare_2.png)

## 4. Assemble `chip` and `sensor tile` to the `bare module`

![assemble chip and sensor](../images/qc-flow/register_bare_3.png)

!!! Warning
    QC-helper can not assemble single chip to bare module. So for this tutorial, we assemble a sensor tile with QC-helper and a chip with web page for ITkPD: [My Components](https://itkpd-test.unicorncollege.cz/myComponents)


After registering a bare module to ITkPD, we can register a new module to ITkPD.

Go to next step.<br>
[Register a New Module to ITkPD](register_module.md)<br>
