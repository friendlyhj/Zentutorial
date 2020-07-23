# 熔炉配方

## **添加**

基本格式：`furance.addRecipe(output, input, xp);`

output输出，input输入，xp为给予经验（使用双精度浮点数，即可用小数，可以省略）

## **移除**

基本格式：`furance.remove(output, input);`

移除将input烧成output的熔炉配方，input可省略，这样指删除所有烧成output的配方。

## **熔炉燃料**

基本格式： `furnace.setFuel(input, burnTime);`

将一个物品设置为燃料，并且设定时间，时间采用gametick。煤炭为1600，烧一个物品需要200。将burnTime设置为0即为删除该燃料。

