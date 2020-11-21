---
title: "Self Organized Criticality Economics"
date: 2020-05-23T17:51:39-07:00
draft: false
tags: ["Data Science", "Modeling", "Simulation", "Economics", Python, "Agent-Based Modeling", "Plotly"]

---

### [Self-Organized Criticality Economic Model github repo](https://github.com/gdcutting/SOCEconModel)

### [Project report (PDF) with experimental results and analysis](media/SYSC557Alife-ProjectReport-GDC.pdf)

After finishing my Master's in Systems Science at PSU, I now have some time to work on my website! Over the next few weeks I'm going to be posting some code and links to past projects. I'd like to start with a project from my Artificial Life class this term - it's a simple Agent-Based economic model based on a Self-Organized Criticality mechanism. I've been interested for a while (since I began my graduate studies, originally in economics) in modeling crisis and crash type behavior. Mainstream economics is still largely devoted to an equilibrium-based perspective that does not fully embrace seeing an economy as a highly dynamic Complex Adaptive System (CAS). There is research going on that does not start with the equilibrium view, and valuable work going on with Agent-Based modeling, which allows us to model a system from the bottom up by specifying the fundamental interactions of the micro-elements in the system instead of only the macro or aggregate behavior (such as the relationship between interest rates and income, for example).

Self-Organized Criticality is a very powerful idea which originated from statistical physics but has found wide application in many diverse areas. The idea of SOC is that certain complex systems self-organize to a 'critical' state in which the behavior is maintained in a region of complex unpredictable behavior. SOC seems to explain, for example, the statistical distribution of such natural events as earthquakes which follow a power-law distribution as in the Gutenberg-Richter Law. SOC seems to hold promise for, among other things, perhaps better explaining the dynamics of crashes and other difficult to predict economic events which are not adequately explained by existing models in the field.

I built an ABM in mesa (the python package for agent-based modeling) that uses a criticality mechanism to generate interesting income behavior even in the presence of fixed demand. This is just the start to a large goal of building a robust economic model using criticality, which includes multiple mechanisms of interest (price mechanism, labor market, etc.) and which incorporates machine learning techniques to give a richer picture of how agent interactions yield larger macroeconomic patterns.

There's much more to do with this model in the future, but this is a start. Next I'll put together a small Jupyter notebook which explains the model behavior and shows a few results.

## Project Reading

[Self-Organized Criticality (Scientific American)](media/SOC-ScientificAmerican-Bak-Chen.pdf)

[Aggregate Fluctuations From Independent Sectoral Shocks: Self Organized Criticality In A Model of Production And Inventory Dynamics](media/AggregateFluctuationsSOC-Bak-Chen-Woodford.pdf)

[An Exactly Solved Model Of Self-Organized Critical Phenomena](media/ExactlySolvedModelSOC-Dhar-Ramaswany.pdf)
