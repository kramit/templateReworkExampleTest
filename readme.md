
### readme

Since I have no info on why things dont work or how thing are supposed to work there are different ways of removing the automation and parameterisation of these templates if they are needed to have hard coded information.  (which I am making an assumption is the road block being faced) 

The 2 ways I have done it are below to choose whatever is needed.




### withParams folder

3 template files

A: "vms" template no variables needed on the deployment command, no changes made to the template as all is hard coded

B + C: Used to require a name suffix of 2 and 3 passed to the template parameters by -nameSuffix X on the deployment command, to remove that and make it static added the line "defaultValue":"2" and "defaultValue":"3" this will populate with a value in the template by default and therefore not need the -nameSuffix on the 

The parameters file is common between A B and C and contained 3 params that were passed in



------------------

### noParams folder

Same as withParams but

All params removed and replaced with hard coded variables in all the templates

E.G 

```
"[parameters('adminUsername')]"  is now "[variables('adminUsername')]"
```


------------------

### deployemnt


$rgname is whatever rgname you want it deployed too

withParams

```
New-AzResourceGroupDeployment -ResourceGroupName $rgName -TemplateFile $pwd/az104-06-vms-template.json -TemplateParameterFile $pwd/az104-06-vm-parameters.json 
New-AzResourceGroupDeployment -ResourceGroupName $rgName -TemplateFile $pwd/az104-06-vm-template.json -TemplateParameterFile $pwd/az104-06-vm-parameters.json 
New-AzResourceGroupDeployment -ResourceGroupName $rgName -TemplateFile $pwd/az104-06-vm-template.json -TemplateParameterFile $pwd/az104-06-vm-parameters.json 
```

noParams

```
New-AzResourceGroupDeployment -ResourceGroupName $rgName -TemplateFile $pwd/az104-06-vms-template.json
New-AzResourceGroupDeployment -ResourceGroupName $rgName -TemplateFile $pwd/az104-06-vm-template.json
New-AzResourceGroupDeployment -ResourceGroupName $rgName -TemplateFile $pwd/az104-06-vm-template.json
```

