Analyzing the Financial Health of Middle Market Firms
### Research Direction: Analyzing the Financial Health of Middle Market Firms

By Noah Levine, Patrick Williams, Yuan Wang, Cillian Fisher

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.

## Table of contents
1. [Introduction](#introduction)
2. [Codes](#meth)
3. [Analysis Section](#section3)
4. [Summary](#summary)

## Introduction  <a name="introduction"></a>

The main purpose of this project is to explore the effectiveness and reliability of various financial metrics and valuation multiples in assessing the financial health and performance of middle market companies in the context of mergers and acquisitions (M&A). Specifically, our research aims to identify which financial metrics demonstrate the strongest correlation with commonly used valuation multiples across different economic sectors in the middle market. This will provide clearer investment strategies and enhance financial assessment methodologies, thereby facilitating more informed decision-making in the M&A process.

## Methodology <a name="meth"></a>

Here is some code that we used to develop our analysis. Blah Blah. [More details are provided in the Appendix](page2).
 
Note that for the purposes of the website, you have to copy this code into the markdown file and  
put the code inside trip backticks with the keyword `python`.

```python
import seaborn as sns 
iris = sns.load_dataset('iris') 

print(iris.head(),  '\n---')
print(iris.tail(),  '\n---')
print(iris.columns, '\n---')
print("The shape is: ",iris.shape, '\n---')
print("Info:",iris.info(), '\n---') # memory usage, name, dtype, and # of non-null obs (--> # of missing obs) per variable
print(iris.describe(), '\n---') # summary stats, and you can customize the list!
print(iris['species'].value_counts()[:10], '\n---')
print(iris['species'].nunique(), '\n---')
```

Notice that the output does NOT show! **You have to copy in figures and tables from the notebooks.**

## Analysis Section <a name="section3"></a>

Here are some graphs that we created in our analysis. We saved them to the `pics/` subfolder and include them via the usual markdown syntax for pictures.

![](pics/plot1.png)
<br><br>
Some analysis here
<br><br>
![](pics/plot2.png)
<br><br>
More analysis here.
<br><br>
![](pics/plot3.png)
<br><br>
More analysis.

## Summary <a name="summary"></a>

Blah blah



## About the team

<img src="pics/julio.jpg" alt="julio" width="300"/>
<br>
Julio is a senior at Lehigh studying finance.
<br><br><br>
<img src="pics/don2.jpg" alt="don" width="300"/>
<br>
Don is an assistant professor at Lehigh.


## More 

To view the GitHub repo for this website, click [here](https://github.com/cillianfisher/finalProject).
