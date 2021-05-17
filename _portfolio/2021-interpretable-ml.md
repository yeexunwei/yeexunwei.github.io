---
title: "Lung Cancer Image Classification"
excerpt: "Lung cancer image classification in Python using LIDC dataset. Images are processed using local feature descriptors and transformation methods before input into classifiers.
<br/>
# <img src='/assets/lungcanc.png' alt='' width='500'/>"
collection: portfolio
---

\documentclass[english]{article}
\usepackage{fullpage}
\usepackage{setspace}
\usepackage{hyperref}


\input{preamble}

%opening

\title{CS5339 Project -- Interpretable Machine Learning}
\date{}
\author{Yee Xun Wei A0228597L}

\onehalfspacing

\begin{document}

\maketitle

\section{Introduction} \label{sec:intro}

Machine learning is becoming much more profound in making decisions critical to life, death and personal wellness. However, machine learning models are \emph{black boxes} that find patterns in data without being able to explain their methodology. There is a lack of sufficient techniques to explain and interpret machine learning decisions. Machine learning utilization can be problematic in areas where decisions of models must be explainable due to laws or regulations or where accountability is required. The need to \emph{trust} machine learning is paramount.



\begin{figure}
	\centering
	\includegraphics[width=.5\textwidth]{interpretability_flow}
	\par
	\caption{Evaluation typically compares predictions and ground truth. Predictions alone and  metrics calculated on these predictions might not be suffice for interpretation. \cite{lipton2017mythos} \label{fig:interpretability_flow} } 
\end{figure}

We define \emph{interpretability} as the \emph{ability to explain or to present in understandable terms to a human} \cite{doshivelez2017rigorous}. Broadly, interpretability focuses on the \emph{how}. Before proceeding with a formal description, we discuss why do we need interpretable machine learning:

\begin{itemize}
	\item \emph{Learn about the data}. Models are meant to be a formal representation of the observed data. Machine learning model can be used to provide useful information to human decision makers and help users develop intuition about the prediction problem.
	\item Interpreting a machine learning model enable users to test the causality of the features and help users \emph{debug} appropriately, for example retrain a model with misclassified samples. Interpretability faciilitates
	better model selection and feature engineering.
	\item \emph{Accountability} of machine learning decisions is an open legal problem.
	\item We might feel more comfortable with a well-understood model. Two aspects of \emph{trust}: (1) trusting a prediction, i.e. user trusts a decision and act on it, and (2) trust a model, i.e. user trusts a model to act in a reasonable manner in real scenarios \cite{ribeiro2016why}.
	\item Machine learning models might learn the bias in the training data and provides false insights at the cost of compromising on \emph{fairness}. Produced interpretations can be used as a way to assess whether decisions made automatically conform to ethical standards.
	
\end{itemize}

\section{Interpretable Machine Learning Concepts}

\subsection{Interpretability Techniques}
We identify the different types of interpretability techniques:

\begin{itemize}
	\item \emph{Local} interpretability implies knowing for a particular decision. \emph{Global} interpretability implies knowing the general patterns. We interpret globally for all data points, such as the importance of each variable of the model decisions.
	\item A technique that is \emph{model-specific} is only suitable for use by a particular class of algorithm. \emph{Model-agnostic} techniques work across all types of models.
\end{itemize}

%\begin{itemize}
%	\item Scope
%	\begin{itemize}
%		\item \emph{Local} interpretability implies knowing for a particular decision.
%		\item \emph{Global} interpretability implies knowing the general patterns. We interpret globally for all data points, such as the importance of each variable of the model decisions.
%	\end{itemize}
%	\item Model
%	\begin{itemize}
%		\item A technique that is \emph{model-specific} is only suitable for use by a particular class of algorithm.		\item \emph{Model-agnostic} techniques work across all types of models.
%	\end{itemize}
%\end{itemize}

\subsection{Properties of Interpretable Models}
Models properties fall into two categories \cite{lipton2017mythos}:

\begin{itemize}
	\item {\em Transparency} refers to {\em how does the model work}. We observe transparency at the level of the full model ({\em simulatablity}), at the level of components (e.g. each input, parameter and calculation) ({\em decomposibility}), and at the level of the learning algorithm itself ({\em algorithmic transparency}).
	\item The second relates to {\em post-hoc explanations} which answers the question {\em what can the model tell us}. Examples of post-hoc explanation consists of model generated text explanations, render visualizations of learned representations ,and explanations by example.
	
%	\begin{itemize}
%		\item {\em Simulatability} implies transparency at the level of the entire model. 
%		\item {\em } at the level of individual components
%	\end{itemize}
\end{itemize}

\subsection{Interpretability vs. Completeness}
Ideally, we want an explanation to be \emph{interpretable} (understandable to humans) and \emph{complete} (describe the decisions of a system in an accurate way) \cite{gilpin2019explaining}. Accurate decisions are not easily interpretable; and conversely the most easily interpretable descriptions may not be the most accurate.



\section{Inherently Interpretable Models}
The easiest way to achieve interpretability is to use interpretable models, i.e. linear regression and decision tree.

\subsection{Linear Regression}
For linear models such as linear and logistic regression, we measure the importance from the weights $w_i$ of each feature $x_i$. For normalized data, $w_i$ represents the important 
model-specific technique that can be used for both global and local explanations.

\begin{equation}
	\hat{y} = w_0 + \sum_{i} w_i x_i
\end{equation}


Estimated weights come with confidence intervals. Confidence intervals provide information about the "true" weight parameter. For instance, a 95\% confidence interval tells us that the confidence interval would contain the true weight in 95 out of 100 sampled cases, given the linear regression model is the correct model for the data.

Feature importance of linear regression can be obtained by the absolute value of the t-statistic, estimated weight scaled with its standard error. The importance of a feature increases with increasing weight. The feature is less important if the variance is high.

\begin{equation}
	t_{\hat{w}_j} = \frac{\hat{w}_j}{SE(\hat{w}_j)}
\end{equation}
where SE is the standard error.

The weighted sum model of how linear regression makes predictions transparent to users. Linear regression is accepted for predictive modeling and doing inference. However, linear regression is inadequate in modeling nonlinearity of input data.

\subsection{Logistic Regression}

Logistic regression is a generalized linear model (GLM) that has similar benefits as linear regression when interpreting model weights. The weighted sum is transformed by the logistic sigmoid function to a probability.

\begin{equation}
	P(y^{(i)} = 1) = \frac{1}{1 + e^{w_0 + w_1 x^{(i)}_1 + ... + w_j x^{(i)}_j}}
\end{equation}

We examine the relationship between predictions and the odds. The odds of an event (i.e. an instance is classified as $y = 1$) are written as the probability of event divided by probability of no event.

\begin{equation*}
	\frac{P(y = 1)}{1 - P(y=1)} = odds = exp(b + \sum_{j} w_p x_p)
\end{equation*}

Increasing a feature by 1 will result in the following odds ratio:

\begin{equation}
	\frac{odds_{x_j + 1}}{odds} = \frac{exp(w_0 + w_1 x_1 + ... + w_j (x_j + 1)  + ... + w_p x_p)}{exp(w_0 + w_1 x_1 + ... + w_j x_j + ... + w_p x_p)}
\end{equation}

We apply the following rule:
\begin{equation}
	\frac{exp(a)}{exp(b)} = exp(a - b)
\end{equation}

\begin{equation}
	\frac{odds_{x_j + 1}}{odds} = exp(w_j(x_j + 1) - w_j x_j) = exp(w_j)
\end{equation}

Increasing a feature $x_j$ by 1 will scale the odds by a factor $exp(w_j)$.




\subsection{Decision Tree}
Decision tree is an explanation family similar to decision rules. Decision tree is structured as a graph where there is a split for each feature (node) according to cutoff values. The classification and regression trees (CART) algorithm is a popular algorithm which takes a feature and determine which cutoff values minimizes the variance of $y$.

We  track how decisions are made from the root node to the leaf node. This is model specific techniques used for local explanations of a decision tree model.

\begin{equation}
	\hat{f}(x) = \bar{y} + \sum_{d=1}^{D} split.contrib(d,x) = \bar{y} + \sum_{j=1}^{p} feat.contrib(j,x)
\end{equation}

We explain an individual prediction by adding contributions of each node. We add contributions of $p$ features to explain how much each feature contributed to a prediction. The root node predicts the mean of the outcome of the training data $\bar{y}$.

Feature importance is used for deep decision tree to interpret the importance of each feature at a global level. The overall importance of a feature in a decision tree can be computed by going through all the splits for which the feature is used and measure how much it has reduced the variance.

Decision tree is suitable to capture relationships between data and features. The tree structure has a natural visualization of nodes and edges. The explanations for each instances is simple since it falls into the binary decisions of each nodes. However, decision tree is inefficient to deal with linear data. Decision tree can become uninterpretable if the tree becomes deep. The maximum number of terminals is $2^{d}$ where $d$ is the depth of tree.

%\begin{equation}
%	\frac{N_{parent}}{N}(Gini_{parent} - \frac{N_{Right}}{N_{parent}} \cdot Gini_{Right} - \frac{N_{Left}}{N_{parent}} \cdot Gini_{Left})
%\end{equation}

%\subsection{Model Agnostic Techniques}
%Some machine learning models are hard to interpret. A deep neural network for example, can have millions of learned parameters.
%
%\subsubsection{Local Surrogate Method}
%approximate the predictions of a black-box model.
%
%\begin{enumerate}
%	\item Get predictions from the black-box model.
%	\item Select an interpretable model (e.g. linear, decision tree)
%	\item Train an interpretable model on the original dataset and use black-box predictions as the target
%	\item measure the performance of the surrogate model.
%\end{enumerate}


\section{LIME (Local Interpretable Model-Agnostic Explanations)}
Local Interpretable Model-Agnostic Explanations (LIME) \cite{ribeiro2016why} is a technique to provide explanations for individual predictions as a solution to "trust the model" problem. The key idea is to locally approximate a black-box model by an interpretable model (\emph{local surrogate model}). LIME is a model-agnostic model which approximates the underlying model $f$ by perturbing the input and observe the prediction changes.

We want to find a locally interpretable model for a black-box model $f(x)$ around the instance of interest $x$. $f(x)$ is the probability that $x$ belongs to a certain class, $f : \mathbb{R}^d \to \mathbb{R}$. $G$ is a class of potential \emph{interpretable} models such as linear models and decision trees. We minimize a loss function:

\begin{equation}{}
	\xi(x) = \argmin_{g \in G} \mathcal{L}(f, g, \pi_x) + \Omega(g)
	\label{eq:lime}
\end{equation}

Model $g \in G$ is $\{0, 1\}^{d'}$ which acts over absence/presence of the \emph{interpretable components}. $\pi_x(z)$ denotes the proximity measure between an instance $z$ to $x$, as to define locality around $x$ (how large the neighborhood around $x$). We let $\mathcal{L}(f, g, \pi_x)$ be a measure of how unfaithful $g$ is in predicting $f$ in the locality defined by $\pi_x$ (how well the interpretable model approximates the black-box model). We add a regularizer $\Omega(g)$ be a penalty for the \emph{complexity} of model $g$, i.e. for decision trees $\Omega(g)$ may be the depth of the tree, for linear models $\Omega(g)$ may be the number of non-zero weights.

We denote $x \in \mathbb{R}^d$ be the original representation of an instance and $x' \in \{0, 1\}^{d'}$ to denote a binary vector for its interpretable representation ("space for the interpretable representation").  

LIME makes the assumption that every complex model is linear on a local scale. We minimize $\mathcal{L}(f, g, \pi_x)$ while having $\Omega(g)$ be low enough to be interpretable. Different explanation families $G$, fidelity functions $\mathcal{L}$ and complexity measures $\Omega.$

We approximate $\mathcal{L}(f, g, \pi_x)$ by drawing non-zero samples around $x'$ uniformly at random. Given a perturbed sample $z' \in \{0, 1\}^{d'}$ (artificial data), we recover the instance in the original representation $z \in \mathbb{R}^d$ and acquire $f(z)$ which is used as a \emph{label} for the explanation model. The intuition behind LIME is depicted in Figure \ref{fig:lime}. Instances both close to $x$ (high weight from $\pi_x$) and far away from $x$ (low weight from $\pi_x$) are sampled to capture the locality.

\begin{figure}
	\centering
	\includegraphics[width=.5\textwidth]{lime}
	\par
	\caption{The black-box model's decision function is represented by the blue/pink background. We want to understand the factors influencing the black-box model around a single instance of interest (bold red cross).  LIME samples instances, get approximation using $f$ and weighs them by the proximity to the instance being explained. The size of the data points corresponds to the proximity. The dashed line  is the interpretable model which serves as a "local explainer" for the specific instance. \cite{ribeiro2016why} \label{fig:lime} } 
\end{figure}

%The general approach of LIME is as follows:
%\begin{enumerate}
%	\item Generate $N$ perturbed instances to explain $\hat{y}$. Let ${z'_i \in X' | i=1,...,N}$ be the set of observations.
%	\item Recover the perturbed instances. Let ${z_i \equiv h^y(z'_i \in X | i=1,...,N)}$ be the original representation.
%	\item Black box model predict hte outcome ief${z'_i \in X' | i=1,...,N}$
%\end{enumerate}

\subsection{Interpretable data representation}
LIME is applicable on tabular data, text and image. Continuous variables in tabular data are discretized to obtain categorical data. We use bag of words and set a limit $K$ on the number of words, i.e. $\Omega(g) = \infty \mathbb{1}[\Vert w_g \Vert_0 > K]$ for text classification. "Super-pixels" (any standard algorithm) is used instead of words for image classification. This particular choice of $\Omega$ makes Eq.~\eqref{eq:lime} intractable. However we approximate $\Omega$ by initially selecting $K$ features with Lasso and then learning the weights via least squares.

%\begin{figure}
%	\centering
%	\includegraphics[width=.8\textwidth]{explain_lime}
%	\par
%	\caption{The black-box model's decision function is represented by the blue/pink background. The bold red cross is the instance being explained. LIME samples instances, get approximation using $f$ and weighs them by the proximity to the instance being explained. The dashed line is the learned explanation local to the specific instance. \cite{oreilly} \label{fig:explain_lime} } 
%\end{figure}

\subsection{Submodular Pick for Explaining Models}
Global understanding of the model is achieved by explaining a set of individual instances. These instances are to be selected judiciously since we may not have the time to examine a large number of explanations. Budget $B$ denotes the number of explanations we are willing to look at under to understand the model. We should pick a representative set of explanations, i.e. non-redundant explanations to represent the global model behavior.

Given the explanations for a set of instances $X$ ($\vert X \vert = n$), we construct an $n \times d'$ \emph{explanation matrix} $\mathcal{W}$. $\mathcal{W}$ implies the local importance of the interpretable components for each instance. We set $\mathcal{W}_{ij} = |w_{g_{ij}}|$ for an instance $x_i$ and explanation $g_i = \xi(x_i)$. $I_j$ (column $j$) denotes the \emph{global} importance of that component.

We formalize the non-redundant coverage intuition in Eq.~\eqref{eq:coverage}. Set function $c$, given $\mathcal{W}$ and $I$, calculates the total importance of the features that appear in at least one instance in a set $V$.

\begin{equation}
	c(V, \mathcal{W}, I) = \sum_{j=1}^{d'} \mathbb{1}_{[\exists i \in V : \mathcal{W}_{ij} >0]} I_j
	\label{eq:coverage}
\end{equation}

Eq.~\eqref{eq:submodular} is maximizing a weighted coverage function, finding the set $V$, $|V| \le B$ that achieves highest coverage.

\begin{equation}
	Pick(\mathcal{W}, I) = \argmax_{V,|V| \leq B} c(V, \mathcal{W}, I)
	\label{eq:submodular}
\end{equation}

\subsection{Experimental Example}
\begin{figure}
	\centering
	\includegraphics[width=.6\textwidth]{image_explanation_dog}
	\par
	\caption{Explaining an image classification prediction using Google's Inception neural network. The predicted class is "Dalmatian" with $p(0.99)$. \label{fig:image_explanation} } 
\end{figure}

In Figure \ref{fig:image_explanation} the super-pixels with positive weight towards the predicted class is highlighted. The neural network picks up the outline of the predicted class "Dalmatian". This kind of explanation enhances trust in the model (regardless whether the prediction is correct or wrong) as the classifier shows to be acting in a reasonable manner.

\subsection{Linear LIME and Shapley Values}
SHAP (SHapley Additive exPlanation) is a game theoretic approach to explain the decision of a model \cite{lundberg2017unified}. The goal is to explain the prediction for $x_i$ as a sum of contributions from individual feature values.

We estimate the SHAP values with weighted linear regression model as the local surrogate model and an appropriate weighting kernel. The Shapley kernel to obtain SHAP values is given by:

\begin{equation}
	\pi_{x'}(z') = \frac{M-1}{(M choose |z'|)|z'|(M-|z'|)},
\end{equation}

where $M$ is the number of features and $|z'|$ is the number of non-zero features in $z'$. 

\section{Discussion}
Linear models are not necessarily more interpretable \cite{lipton2017mythos}. A decision tree with billions of nodes, for instance, may be challenging to understand.

Explaining interpretations requires prior knowledge and human-based evaluations of explanations could be misleading because of bias. A reasonable explanation provided for a model decisions does not necessary be reflective of what the model is doing.

Through model or post-hoc interpretability, we might be able to understand how a model make a prediction. Yet we are unable to understand the model if the data representation of the underlying model is not explainable.

A limitation of LIME is that an interpretable model is selected to approximate the black box, not the data. The most useful applications of LIME is to define a low-dimensional interpretable data representation from high-dimensional data.

\newpage
\nocite{*}
\bibliographystyle{plain}
\bibliography{refs}

\end{document}
