# Annoucing `pyns.fetch_utils`-- a simple API for fetching Neuroscout data, and new encoding model tutorials

```{post} 2023-04-7
:author: Alejandro de la Vega
:tags: newsletter, encoding, pyns, api
:excerpt: 2
```

Neuroscout makes it easy to create and share fully reproducible fMRI analyses using a fully web-based interface. However, there are tradeoffs between *ease of use and flexibility*. To make Neuroscout easy to use, we have to make assumptions about the types of analyses that users want to perform. We ensure reproducibility by only allowing users to perform analyses that can be fully specified by [BIDS Stats Models](https://bids-standard.github.io/stats-models/), and are executable by [FitLins](https://fitlins.readthedocs.io/en/latest/). Currently, this means multi level GLM analyzes using predictors pre-extracted and indexed by the Neuroscout API.

As a consequence, there will always be newer types of analyses that are not possible to specify using the web-based Neuroscout interface. This can be a challenge for naturalistic data in particular, as this area of research is rapid evolving and new analyses are constantly being developed. Although we have plans to continously expand the types of analyses that can be performed on Neuroscout (and in turn BIDS Stats Model and FitLins), there will always be analyses that are not possible to perform in a centralized fashion using a web interface.

## New utilities for fetching Neuroscout data 🛠️

To address this limitation, we have released a new set of API utilities (`pyns.fetch_utils`) that allow users to easily fetch data from the Neuroscout API for custom analysis. 🎉 

This new addition allows users to fetch both predictors and brain imaging time courses from Neuroscout using a simple, uniform API. 

As a reminder, Neuroscout indexes over a dozen openly available neuroimaging datasets (browse here: https://neuroscout.org/datasets), and for each dataset we extract hundreds of predictors (browse here: https://neuroscout.org/predictors). All of these predictors are centrally indexed by Neuroscout, and made publicly available using a uniform API, which can be accessed using the [pyNS](https://pyns.readthedocs.io/en/latest) Python client.

The new `pyns.fetch_utils` utilities make this process even easier by providing a simplified user interface, and performing common transformations to make the data readily usable.

`fetch_predictors` allows users to fetch several predictors from any of the indexed datasets simultaneously using a simple API, and optionally apply transformations using the `pybids.modeling` tools (like you would in BIDS Stats Models). For example, you can easily resample the predictors to TR (which may be sampled at different rates), rescale them, and align them to the fMRI timecourse. 

`fetch_images` allows users to download preprocessed brain imaging time courses from any of the indexed datasets (with the help of [DataLad](https://www.datalad.org/) that align with the predictors.

With a set of predictors, and a set of brain imaging time courses, users can then easily fit any custom analysis they want using their favorite machine learning library, such as [nilearn](https://nilearn.github.io/stable/) or [scikit-learn](https://scikit-learn.org/stable/). 

To learn more about `pyns.fetch_utils`, check out the [documentation](https://pyns.readthedocs.io/en/latest/fetching.html).

## Encoding model tutorials! 🚀

To demonstrate how to use `pyns.fetch_utils`, we have created two new example notebooks that demonstrate how to fit a simple voxelwise encoding model using the new API fetch utilities. 

In the first example, we implement a cross-validated voxelwise encoding model for a single subject using ridge regression implemented in [Himalaya](https://github.com/gallantlab/himalaya). In the second example, we fit two feature sets jointly in the same model using a technique known as banded ridge regression. These techniques are very useful for fitting high dimensional feature sets to fMRI data, which is particularly useful for naturalistic data.

These example were based on the fantastic [voxelwise modeling tutorials](https://gallantlab.org/voxelwise_tutorials/) by the Gallant Lab , so be sure to check out their tutorials if you are interested in learning more about voxelwise encoding models for fMRI data. 

Check out the examples [in the Neuroscout Docs tutorials](https://neuroscout.github.io/neuroscout-docs/python_api/tutorials.html), and follow along in the cloud using Google Colab by clicking on the 🚀.

## Where to go from here? 

We hope `pyns.fetch_utils` will help you create your own custom workflows using the Neuroscout platform.

However, be aware we are actively working on expanding the types of analyses that can be performed on Neuroscout, with a focus on adding support for voxelwise encoding models in BIDS Stats Models and [Neuroscout-CLI](https://neuroscout-cli.readthedocs.io/en/latest/).

Also, note that by implementing a custom pipeline, your analysis will not be centrally registered on neuroscout.org, and a reproducible record will not be made. For analyses supported the [Neuroscout-CLI](https://neuroscout-cli.readthedocs.io/en/latest/), it is recommended to use the neuroscout.org web interface, or follow the guide for programmatically creating analyses using [pyNS](https://pyns.readthedocs.io/en/latest/analyses.html).

Finally, if you develop a workflow using `pyns.fetch_utils`, we would love to hear about it, so we can help you share it with the community!

Be sure to stay tuned for more updates, and get in touch if you want to contribute!

## Acknowledgements

Thank you to Roberta Rocca and Sam Nastase for their help in developing the example encoding model notebook during the 2022 OHBM Hackathon!
Also thank you to Jeff Mentch, for his help in developing the `pyns.fetch_utils` API, and giving feedback on the Neuroscout platform.
