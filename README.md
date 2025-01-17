# CC-Research

My research goal is to build an emulator (i.e., surrogate) for the Water Erosion Predictor Project (WEPP) model using Gaussian processes and to increase runtime rate required to get a spatio-temporal distribution of soil loss across one specific field. We build a surrogate on a hierarchical Gaussian processes. We chose an exponential covariance function with the highly correlated weight parameters to assess the correlation within the response given the correlation between the functional inputs. We assume that weight parameters come from autoregressive model. Additionally, the model employs an empirical Bayes approach for parameters estimation.




## Backlog
- Write a function to assess the runtime of optim() ~ benchmark
- Create a new file that contains all assumptions and estimation process
- Choose font, size and style for the paper
- Outline: How many pages, tables, figures and parts
- (!)Correct the log_likelihood_with_penalty >>> make p(w) look like the one you used in simulation
- Run the simulation and estimation on for T = 365 on server
- Use thesis template and put everything together into one!!!!!!!




## In-progress
- Following R-style guide
- Writing an abstract
- Writing log process of optimization

- Collect the simulated data from STRIPS-1
- Sensitivity analysis using paper of Prof. Morris
- Try Prof. Morris's approach: use basis functions, dlm R-package, "Dynamic Linear Models with R" on Time Series. Choose optimal q = number of harmonics, where harmonics come in pairs. So you will have 2q number of parameters to estimate instead of 365. Book pages: {102, 103, 108} 
- Trying to run code on smaster




## Done
- Increased the penalty: rho = 0.99
- Set white noise variance: sigmasq = 1 
- Changed w(t) from deterministic to sampled
- Simulated w(t) from truncated distribution
- Splitted weight_predictor() and loglkl_with_penalty() into separate files
- Separated simulation from functions and other constants
- A separate new "log" document was created to keep track of changes and experiments with simulated data and preliminary model assumptions
- Removed constants from functions
- Plotted 3D of loglkl_with_penalty holding all but two constant (too lengthy)
- Wrote a function to assess the accuracy of loglkl_with_penalty() with different pars, gradients
- Changed w(t) into log scale: log(w) ~ MVN centered at -1 or -2
- Matrix differentiation techniques: Book(yes)/article(yes)/Wolfram Alpha(no need) - probably download
- Derived the real gradient function for maximization of loglkl_with_penalty()
- Updated gradient function code
- Tried new pars: simulated from AR(1)
- Found MoM estimators of weights: techniques, don't work well as I wanted
- Found a new distribution which takes into account facts about weights: 1. High correlation 2.Concentration around zero 3.Positiveness :Beta autoregressive process -- did not work since it is spiky
- Tried Tempering method suggested by Prof. Niemi
- Decide on the optimal sample size: 100 < n < 200 for w(t) ~ AR(1)




### Comments: (01/14/19)
- Tried to transform weights:w into log scale, found induced distribution, but had some difficulties: 1.Proposal distribution 2.Stan
- New weights sampled using log(w) dist with the same covariance matrix are reasonably good. Estimates are fair enough with the initial values as true values. However, another pars gives different results, so optim() might be converging to local maxima again. Remedy?
- Found (?)appropriate process for weights, as Beta AR(1), don't know how to implement this idea? >> more research
- When T >> 250 optim() is not simply working, since \Pi and \Omega are becoming ND. Remedy?
- Tried new (true) gradient: estimates with initial values as true weights are exactly the same as with numerical gradient. However, there is a significant improvement in the runtime of optim() (!!!)

### Comments: (02/04/19)
- Deriving the gradient: changed the precision matrix. It should optimize the code and decrease the runtime. 
- We changed the assumption that weights have to be within [0,1], while they probably will fall into this range, the real range is [0, \infty]

### Comments: (02/11/19)
- There are three types of data: true, simulated, emulated
- For some reason, dividing and splitting wasn't giving good results -- actually it went crazy
- Miller's thesis contains sufficient information for the data generation
- Abstract should be 12-30 pages without pictures and tables
- There is a thesis template on the page of Prof. Niemi
- You can code part containing MLE optim to the paper
- Small steps do not have to be included in the paper
