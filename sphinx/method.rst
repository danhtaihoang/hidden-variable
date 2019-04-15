Method
===========================

| When the configuration of an entire system is observed, we can apply
  our method, Expectation Reflection (ER) [formerly Free Energy Minimization (FEM)], to infer the interactions
  :math:`W_{ij}` between variables. Briefly, This method uses an iterative algorithm to update the model of the influence on each position from other positions according to the ratio of the observation to the corresponding model expectation. This approach completely separates model updates from minimization of a cost function measuring goodness of fit, so that this cost function can be used as the stopping criterion of the iteration. The algorithm of ER method contains the following steps:
| (i) Initialize :math:`W_{ij}` at random;
| (ii) Compute local field :math:`H_i(t) = \sum_j W_{ij} \sigma_j (t)`;
| (iii) Update the local field:
  :math:`H_i^\text{new}(t) = \sigma_i(t+1) / \langle  \sigma(t+1) \rangle_{\text{model}} H_i(t),`
  where :math:`\langle  \sigma(t+1) \rangle_{\text{model}}` represents
  model expectation. For binary variables,
  :math:`\langle  \sigma(t+1) \rangle_{\text{model}} = \tanh H_{i}(t)`;
| (iv) Extract coupling
  :math:`W_{ij}^\text{new}= \sum_k \langle \delta H_i^\text{new} \delta \sigma_k  \rangle [C^{-1}]_{kj},`
  where :math:`\langle \cdot \rangle` represents sample mean,
  :math:`\delta f \equiv f -\langle f\rangle` and
  :math:`C_{jk} \equiv \langle \delta\sigma_j\delta\sigma_k\rangle;`
| (v) Repeat (ii)-(iv) until the discrepancy between observed
  :math:`\sigma_i(t+1)` and model expectation
  :math:`\langle  \sigma(t+1)  \rangle_{\text{model}}`,
  :math:`D_i(W)\equiv\sum_{t} \big[ \sigma_i(t+1) - \langle \sigma_i(t+1) \rangle_{\text{model}} \big]^2`
  starts to increase;
| (vi) Compute (ii)-(iv) in parallel for every index
  :math:`i \in \{1, 2, \cdots, N\}`.

| As described in the model section, the aim of this work, however, was
  to consider a situation in which observed data contains only subset of
  variables, the configurations of hidden variables are invisible. Here,
  we developed an iterative approach to update the configurations of
  hidden variables based on configurations of observed variables as the
  following:
| (i) Assign the configurations of hidden variables at random;
| (ii) Infer coupling weights :math:`W_{ij}` including
  observed-to-observed, hidden-to-observed, observed-to-hidden, and
  hidden-to-hidden interactions from the configurations of variables by
  using the ER method;
| (iii) Flip the state of hidden variables with a probability
  :math:`\mathcal{L}_{2} /(\mathcal{L}_{1}+\mathcal{L}_{2})` where
  :math:`\mathcal{L}_{1}` and :math:`\mathcal{L}_{2}` represent the
  likelihood :math:`\mathcal{L}` of systems before and after the flipping,

  .. math:: {\cal{L}} = \prod_{t=1}^{L-1}\prod_{i=1}^{N} P[\sigma_i(t+1)|\sigma(t)] ;
| (iv) Repeat steps (ii) and (iii) until the discrepancy of observed
  variables becomes saturated. The final value of :math:`W_{ij}` and
  hidden variables are our inferred coupling weights and configurations
  of hidden spins, respectively.

To estimate the number of hidden variables, we first calculate the
discrepancy of entire system

.. math:: D = \frac{D_{\text{obs}}}{N_{\text{obs}}} (N_{\text{obs}} + N_{\text{hidden}})
where :math:`D_{\text{obs}}` represents the discrepancy between observations and model expectations,
:math:`D_{\text{obs}} = \sum_{t} \big[ \sigma_i(t+1) - \langle \sigma_i(t+1) \rangle_{\text{model}} \big]^2` (
:math:`i \in`  observed variables), 
:math:`N_{\text{obs}}` and
:math:`N_{\text{hidden}}` represent number of observed and hidden
variables, respectively. The number of hidden variables corresponds to
the minima of the discrepancy of entire system :math:`D`.
