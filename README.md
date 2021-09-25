# mlse2020-workshop 
Tutorial Workshop: Machine Learning in Materials Science, Dec 13-15, 2020: https://www.eventbrite.com/e/tutorial-workshop-machine-learning-in-materials-science-tickets-128297271593


See also: Strategies for the Construction of Neural-Network Based Machine-Learning Potentials (MLPs),
A.M. Miksch*, T. Morawietz, J. Kästner, A. Urban, N. Artrith*, 
“Strategies for the Construction of Machine-Learning Potentials for Accurate and Efficient Atomic-Scale Simulations”, Mach. Learn.: Sci. Technol. 2 **(2021)** 031001. DOI: https://doi.org/10.1088/2632-2153/abfd96 <br/>
Or https://github.com/atomisticnet/MLP-beginners-guide <br/>
Contact: Nong Artrith (nartrith@atomistic.net)

**SUNDAY, DECEMBER 13 – DATA FROM SIMULATION**

9:00 AM - 9:30 AM: Overview: Machine Learning for Materials Science: Alexander Urban, Columbia University

9:30 AM - 11:00 AM: Artificial Neural Network Potentials for Materials: Nongnuch Artrith, Columbia University

The link to the ænet Google Colab notebook is:
https://colab.research.google.com/drive/1Uz3xulDPMoAEHj1RNPYdq-fAwBwId-aB?usp=sharing

Contact: Nong Artrith (nartrith@atomistic.net) and Alex Urban (aurban@atomistic.net)

To learn more about ænet, sign up to the [Google Group](https://groups.google.com/forum/#!forum/aenet)
so that you don’t miss any announcements (e.g., for new releases) and can reach
a wider community with any questions/issues related to ænet.
Once subscribed, you can also post by sending emails to aenet@googlegroups.com.

## Example of construction and application of ANN potentials

This directory contains an example that showcases the **Chebyshev
descriptor** for local atomic environments proposed in
[*Phys. Rev. B* **96** (2017)
014112](http://dx.doi.org/10.1103/PhysRevB.96.014112).

Owing for the large amount of data the reference data set and the
training set files are not included in the example.  Otherwise the
example is self-contained.  The reference data set used is the
TiO<sub>2</sub> data set from [*Comput. Mater. Sci.* **114** (2016)
135-150](http://dx.doi.org/10.1016/j.commatsci.2015.11.047), which can
be downloaded from
[ann.atomistic.net](http://ann.atomistic.net/download/).  Using that
data set, the training set file can be generated as described in the
first subdirectory `01-generate`.

Output files generated at each step are contained in `output`
subdirectories.

01-generate
-----------

Evaluation of the Chebyshev descriptor for all structures in the
reference data set.  The resulting feature vectors are written to a
*training set* file.

- `generate.in`: Input file for `generate.x`
- `O.fingerprint.stp` and `Ti.fingerprint.stp`: Descriptor definitions
  for the atomic species O and Ti.  For both species relatively small
  descriptor sizes with a radial expansion order of 16 and an angular
  order of 4 are used for set001 and set002.  Another set (set003) uses
  different order of expansions: radial 22 and angular 6.

02-train
--------

Training examples using the *training set* files generated in the
previous step (not included because of the file size).  The results of
three training runs with different neural network sizes are shown in the 
subdirectories `set001`, `set002`, and `set003`.

- `train.in`: Input file for `train.x`
- `get-energies`: Subdirectory demonstrating how to write out the
  energies and errors of all training and testing samples (after
  training has completed).

Training will generate the ANN potential files `O.15t-15t.nn` and
`Ti.15t-15t.nn` which are also provided in the `output` subdirectory.

03-predict
----------

Usage of the ANN potentials trained in the previous step for the
prediction of the entire reference data set.

- `predict.in`: Input file for `predict.x`
- `O.15t-15t.nn` and `Ti.15t-15t.nn`: ANN potential files

The output (energies and atomic forces) can be found in the `output`
subdirectory.

04-aenetLib-ann-md
----------

Usage of the trained ANN potentials from `set003` with external solftware.
Example for the Python (API) with the Atomistic Simulation Environment (ASE).
See the ænet Google Colab notebook.

- `O.40t-40t.nn` and `Ti.40t-40t.nn`: ANN potential files

