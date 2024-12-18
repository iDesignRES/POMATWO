# POMATWO

This README provides an overview of the Model POMATWO within iDesignRES.

It is handled by the Workgroup for Economic and Infrastructure Policy (WIP) at 
TU Berlin  and part of 1, Task number 1.3. 
  
## Purpose of the model  

POMATWO is an electricity market model designed to determine the optimal electricity
supply by minimize system costs on an hourly basis. It incorporates market clearing conditions, market zone-specific merit order curves, 
grid topology, and network constraints. Using a multi-step approach, POMATWO can 
simulate both the electricity generation of the day-ahead market and multiple
intraday market gates. Within the iDesignRES framework, POMATWO is used to 
calculate the cost-optimal utilization of generation capacities.

## Model design philosophy  
The design of POMATWO adopts a multistep approach, emphasizing the structured and 
systematic representation of electricity markets. The workflow consists of distinct 
yet interconnected stages. It begins with the simulation of the day-ahead market,
where electricity generation is allocated cost-efficiently based on the merit-order principle.
This step ensures market clearing conditions are met while minimizing production costs.

In the next step, POMATWO simulates a given number intraday market gates that follow
the day-ahead market. This phase uses updated time series data that forecast solar 
and wind generation profiles, as well as load variations, depending on the time to delivery.
Based on these forecasts, the model recalculates cost-minimal dispatch.
The results are passed to Plan4Res, which performs the final AC redispatch calculations.

POMATWO cantains also feature of performing a DCOPF redispatch to adress grid constraints. 
Using DC optimal power flow calculations, POMATWO determines redispatch actions
necessary to manage congestion, aiming to minimize the extent of these adjustments 
and maintain system stability. This feature is not used for the iDesignRES case study, since an 
AC redispatch is calculated by Pan4Res.

## Input to and output from the model  
To run POMATWO, as it is used in iDesignRES, the following input data set is required: 

- Definition of the market zones, time steps, set of nodes, set of generation technologies 
(incl. solar and wind), set of storages, set of lines 

- Data sets describing the power plants (availability and capacity), the grid 
(capacity of the lines and topographie of the grid), storages (inflow, capacity 
and efficiency factor), marginal costs of each generation technology and the load.
 
POMATWO calculates the cost-optimal usage of generation capacities to meet the load. 
Main outputs are: 

- Generation of each power plant at each time step (MWh)
   
- Change of each storage charging level at each time step (MWh)
  
- Injection at each node at each time step (MWh)
  
These results are available for the day-ahead market at each intraday gate.

## Implemented features  
POMATWO employs a multi-step approach, solving the day-ahead and intraday markets sequentially.
Depending on the specific application, the model can be configured to solve only 
the day-ahead market or both the day-ahead and intraday markets consecutively. While POMATWO 
offers the feature to run redispatch calculation, this feature is optional for the user and is not 
directly included in day-ahead calculations.

## Core assumption  
POMATWO operates under the assumption of perfect foresight, minimizing system costs 
while accounting for the market clearing of zonal markets and adhering to the
merit-order principle. This approach implies an underlying assumption of perfect 
competition in the electricity generation market, where producers are presumed 
to bid at their marginal costs to maximize profits. 

The model is able to determine redispatch actions required to address congestion,
by minimizing the scale of these adjustments to maintain grid stability. 
It is also important to note that the model does not include flexibility costs in its considerations. 

## Repository 
The link to the GitLab repository of the POMATWO model:
https://git.tu-berlin.de/wip/elmodtoolbox/elmod.jl/-/tree/iDesignRES?ref_type=heads
