# saddle_detector
A novel similarity-covariant feature detector that extracts points whose
neighborhoods, when treated as a 3D intensity surface, have a saddle-like
intensity profile. The saddle condition is verified efficiently by intensity
comparisons on two concentric rings that must have exactly two dark-to-bright
and two bright-to-dark transitions satisfying certain geometric constraints.
Saddle is a fast approximation of Hessian detector as ORB detector is for
Harris detector. Experiments show that the Saddle features are general, evenly
spread and appearing in high density in a range of images.

The Saddle detector is among the fastest proposed. In comparison with detector
with similar speed, the Saddle features show superior matching performance on
number of challenging datasets.
