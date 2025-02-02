# Anserini Regression Experiments

Regression experiments in Anserini are hooked into a rigorous end-to-end regression framework driven by the [`run_regression.py`](../src/main/python/run_regression.py) script.
This script automatically runs experiments based on configuration files stored in [`src/main/resources/regression/`](../src/main/resources/regression/), performing the following actions:

+ Building the index from scratch.
+ Verifying index statistics (sanity check that the index has been built properly).
+ Performing retrieval runs with standard settings.
+ Evaluating the runs and verifying effectiveness results.

Furthermore, the regression documentation pages are auto-generated based on [raw templates](../src/main/resources/docgen/templates).

Internally at Waterloo, we are continuously running these regression tests to ensure that new commits do not break any existing experimental runs (see below).
We keep a [change log](regressions-log.md) to document substantive changes.

## The Anserini Reproducibility Promise

It is the highest priority of the project to ensure that all regression experiments are reproducible _all the time_.
This means that anyone with the document collection should be able to reproduce _exactly_ the effectiveness scores we report in our regression documentation pages.

We hold this ideal in such high esteem and are so dedicated to reproducibility that if you discover a broken regression before we do, Jimmy Lin will buy you a beverage of choice (coffee, beer, etc.) at the next event you see him (e.g., SIGIR, TREC, etc.).

Here's how you can help:
In the course of reproducing one of our results, please let us know you've been successful by sending a pull request with a simple note, like what appears at the bottom of [the regressions for Disks 4 &amp; 5 page](regressions-disk45.md).
Since the regression documentation is auto-generated, pull requests should be sent against the [raw templates](../src/main/resources/docgen/templates).
In turn, you'll be recognized as a [contributor](https://github.com/castorini/anserini/graphs/contributors).

## Invocations

Internally at Waterloo, we have two machines (`tuna.cs.uwaterloo.ca` and `orca.cs.uwaterloo.ca`) for the development of Anserini and is set up to run the regression experiments.

Copy and paste the following lines into console to run the regressions from the raw collection:

```bash
nohup python src/main/python/run_regression.py --index --verify --search --regression disk12 >& logs/log.disk12 &
nohup python src/main/python/run_regression.py --index --verify --search --regression disk45 >& logs/log.disk45 &
nohup python src/main/python/run_regression.py --index --verify --search --regression robust05 >& logs/log.robust05 &
nohup python src/main/python/run_regression.py --index --verify --search --regression core17 >& logs/log.core17 &
nohup python src/main/python/run_regression.py --index --verify --search --regression core18 >& logs/log.core18 &

nohup python src/main/python/run_regression.py --index --verify --search --regression mb11 >& logs/log.mb11 &
nohup python src/main/python/run_regression.py --index --verify --search --regression mb13 >& logs/log.mb13 &

nohup python src/main/python/run_regression.py --index --verify --search --regression wt10g >& logs/log.wt10g &
nohup python src/main/python/run_regression.py --index --verify --search --regression gov2 >& logs/log.gov2 &
nohup python src/main/python/run_regression.py --index --verify --search --regression cw09b >& logs/log.cw09b &
nohup python src/main/python/run_regression.py --index --verify --search --regression cw12b13 >& logs/log.cw12b13 &
nohup python src/main/python/run_regression.py --index --verify --search --regression cw12 >& logs/log.cw12 &

nohup python src/main/python/run_regression.py --index --verify --search --regression car17v1.5 >& logs/log.car17v1.5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression car17v2.0 >& logs/log.car17v2.0 &
nohup python src/main/python/run_regression.py --index --verify --search --regression car17v2.0-doc2query >& logs/log.car17v2.0-doc2query &

nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage >& logs/log.msmarco-passage &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-wp >& logs/log.msmarco-passage-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-doc2query >& logs/log.msmarco-passage-doc2query &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-docTTTTTquery >& logs/log.msmarco-passage-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-deepimpact >& logs/log.msmarco-passage-deepimpact &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-unicoil >& logs/log.msmarco-passage-unicoil &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-unicoil-noexp >& logs/log.msmarco-passage-unicoil-noexp &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-unicoil-tilde-expansion >& logs/log.msmarco-passage-unicoil-tilde-expansion &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-distill-splade-max >& logs/log.msmarco-passage-distill-splade-max &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-passage-splade-distil-cocodenser-medium >& logs/log.msmarco-passage-splade-distil-cocodenser-medium &

nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc >& logs/log.msmarco-doc &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-wp >& logs/log.msmarco-doc-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-docTTTTTquery >& logs/log.msmarco-doc-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-segmented >& logs/log.msmarco-doc-segmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-segmented-wp >& logs/log.msmarco-doc-segmented-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-segmented-docTTTTTquery >& logs/log.msmarco-doc-segmented-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-segmented-unicoil >& logs/log.msmarco-doc-segmented-unicoil &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-doc-segmented-unicoil-noexp >& logs/log.msmarco-doc-segmented-unicoil-noexp &

nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-passage >& logs/log.dl19-passage &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-passage-wp >& logs/log.dl19-passage-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-passage-docTTTTTquery >& logs/log.dl19-passage-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-passage-unicoil >& logs/log.dl19-passage-unicoil &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-passage-unicoil-noexp >& logs/log.dl19-passage-unicoil-noexp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-passage-splade-distil-cocodenser-medium >& logs/log.dl19-passage-splade-distil-cocodenser-medium &

nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc >& logs/log.dl19-doc &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-wp >& logs/log.dl19-doc-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-docTTTTTquery >& logs/log.dl19-doc-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-segmented >& logs/log.dl19-doc-segmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-segmented-wp >& logs/log.dl19-doc-segmented-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-segmented-docTTTTTquery >& logs/log.dl19-doc-segmented-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-segmented-unicoil >& logs/log.dl19-doc-segmented-unicoil &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl19-doc-segmented-unicoil-noexp >& logs/log.dl19-doc-segmented-unicoil-noexp &

nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-passage >& logs/log.dl20-passage &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-passage-wp >& logs/log.dl20-passage-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-passage-docTTTTTquery >& logs/log.dl20-passage-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-passage-unicoil >& logs/log.dl20-passage-unicoil &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-passage-unicoil-noexp >& logs/log.dl20-passage-unicoil-noexp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-passage-splade-distil-cocodenser-medium >& logs/log.dl20-passage-splade-distil-cocodenser-medium &

nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc >& logs/log.dl20-doc &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-wp >& logs/log.dl20-doc-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-docTTTTTquery >& logs/log.dl20-doc-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-segmented >& logs/log.dl20-doc-segmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-segmented-wp >& logs/log.dl20-doc-segmented-wp &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-segmented-docTTTTTquery >& logs/log.dl20-doc-segmented-docTTTTTquery &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-segmented-unicoil >& logs/log.dl20-doc-segmented-unicoil &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl20-doc-segmented-unicoil-noexp >& logs/log.dl20-doc-segmented-unicoil-noexp &

nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-passage >& logs/log.msmarco-v2-passage &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-passage-d2q-t5 >& logs/log.msmarco-v2-passage-d2q-t5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-passage-augmented >& logs/log.msmarco-v2-passage-augmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-passage-augmented-d2q-t5 >& logs/log.msmarco-v2-passage-augmented-d2q-t5 &

nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-passage-unicoil-noexp-0shot >& logs/log.msmarco-v2-passage-unicoil-noexp-0shot &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-passage-unicoil-0shot >& logs/log.msmarco-v2-passage-unicoil-0shot &

nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc >& logs/log.msmarco-v2-doc &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-d2q-t5 >& logs/log.msmarco-v2-doc-d2q-t5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-segmented >& logs/log.msmarco-v2-doc-segmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-segmented-d2q-t5 >& logs/log.msmarco-v2-doc-segmented-d2q-t5 &

nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-segmented-unicoil-noexp-0shot >& logs/log.msmarco-v2-doc-segmented-unicoil-noexp-0shot &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-segmented-unicoil-noexp-0shot-v2 >& logs/log.msmarco-v2-doc-segmented-unicoil-noexp-0shot-v2 &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-segmented-unicoil-0shot >& logs/log.msmarco-v2-doc-segmented-unicoil-0shot &
nohup python src/main/python/run_regression.py --index --verify --search --regression msmarco-v2-doc-segmented-unicoil-0shot-v2 >& logs/log.msmarco-v2-doc-segmented-unicoil-0shot-v2 &

nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-passage >& logs/log.dl21-passage &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-passage-d2q-t5 >& logs/log.dl21-passage-d2q-t5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-passage-augmented >& logs/log.dl21-passage-augmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-passage-augmented-d2q-t5 >& logs/log.dl21-passage-augmented-d2q-t5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-passage-unicoil-noexp-0shot >& logs/log.dl21-passage-unicoil-noexp-0shot &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-passage-unicoil-0shot >& logs/log.dl21-passage-unicoil-0shot &

nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc >& logs/log.dl21-doc &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-d2q-t5 >& logs/log.dl21-doc-d2q-t5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-segmented >& logs/log.dl21-doc-segmented &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-segmented-d2q-t5 >& logs/log.dl21-doc-segmented-d2q-t5 &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-segmented-unicoil-noexp-0shot >& logs/log.dl21-doc-segmented-unicoil-noexp-0shot &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-segmented-unicoil-noexp-0shot-v2 >& logs/log.dl21-doc-segmented-unicoil-noexp-0shot-v2 &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-segmented-unicoil-0shot >& logs/log.dl21-doc-segmented-unicoil-0shot &
nohup python src/main/python/run_regression.py --index --verify --search --regression dl21-doc-segmented-unicoil-0shot-v2 >& logs/log.dl21-doc-segmented-unicoil-0shot-v2 &

nohup python src/main/python/run_regression.py --index --verify --search --regression backgroundlinking18 >& logs/log.backgroundlinking18 &
nohup python src/main/python/run_regression.py --index --verify --search --regression backgroundlinking19 >& logs/log.backgroundlinking19 &
nohup python src/main/python/run_regression.py --index --verify --search --regression backgroundlinking20 >& logs/log.backgroundlinking20 &

nohup python src/main/python/run_regression.py --index --verify --search --regression fever >& logs/log.fever &

nohup python src/main/python/run_regression.py --index --verify --search --regression ntcir8-zh >& logs/log.ntcir8-zh &
nohup python src/main/python/run_regression.py --index --verify --search --regression clef06-fr >& logs/log.clef06-fr &
nohup python src/main/python/run_regression.py --index --verify --search --regression trec02-ar >& logs/log.trec02-ar &
nohup python src/main/python/run_regression.py --index --verify --search --regression fire12-bn >& logs/log.fire12-bn &
nohup python src/main/python/run_regression.py --index --verify --search --regression fire12-hi >& logs/log.fire12-hi &
nohup python src/main/python/run_regression.py --index --verify --search --regression fire12-en >& logs/log.fire12-en &

nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-ar >& logs/log.mrtydi-v1.1-ar &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-bn >& logs/log.mrtydi-v1.1-bn &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-en >& logs/log.mrtydi-v1.1-en &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-fi >& logs/log.mrtydi-v1.1-fi &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-id >& logs/log.mrtydi-v1.1-id &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-ja >& logs/log.mrtydi-v1.1-ja &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-ko >& logs/log.mrtydi-v1.1-ko &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-ru >& logs/log.mrtydi-v1.1-ru &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-sw >& logs/log.mrtydi-v1.1-sw &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-te >& logs/log.mrtydi-v1.1-te &
nohup python src/main/python/run_regression.py --index --verify --search --regression mrtydi-v1.1-th >& logs/log.mrtydi-v1.1-th &

nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-trec-covid-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-trec-covid-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-bioasq-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-bioasq-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-nfcorpus-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-nfcorpus-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-nq-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-nq-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-hotpotqa-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-hotpotqa-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-fiqa-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-fiqa-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-signal1m-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-signal1m-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-trec-news-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-trec-news-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-robust04-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-robust04-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-arguana-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-arguana-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-webis-touche2020-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-webis-touche2020-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-android-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-android-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-english-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-english-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-gaming-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-gaming-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-gis-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-gis-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-mathematica-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-mathematica-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-physics-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-physics-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-programmers-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-programmers-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-stats-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-stats-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-tex-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-tex-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-unix-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-unix-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-webmasters-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-webmasters-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-wordpress-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-cqadupstack-wordpress-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-quora-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-quora-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-dbpedia-entity-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-dbpedia-entity-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-scidocs-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-scidocs-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-fever-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-fever-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-climate-fever-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-climate-fever-splade-distil-cocodenser-medium &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-scifact-splade-distil-cocodenser-medium >& logs/log.beir-v1.0.0-scifact-splade-distil-cocodenser-medium &

nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-trec-covid-flat >& logs/log.beir-v1.0.0-trec-covid-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-bioasq-flat >& logs/log.beir-v1.0.0-bioasq-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-nfcorpus-flat >& logs/log.beir-v1.0.0-nfcorpus-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-nq-flat >& logs/log.beir-v1.0.0-nq-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-hotpotqa-flat >& logs/log.beir-v1.0.0-hotpotqa-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-fiqa-flat >& logs/log.beir-v1.0.0-fiqa-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-signal1m-flat >& logs/log.beir-v1.0.0-signal1m-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-trec-news-flat >& logs/log.beir-v1.0.0-trec-news-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-robust04-flat >& logs/log.beir-v1.0.0-robust04-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-arguana-flat >& logs/log.beir-v1.0.0-arguana-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-webis-touche2020-flat >& logs/log.beir-v1.0.0-webis-touche2020-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-android-flat >& logs/log.beir-v1.0.0-cqadupstack-android-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-english-flat >& logs/log.beir-v1.0.0-cqadupstack-english-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-gaming-flat >& logs/log.beir-v1.0.0-cqadupstack-gaming-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-gis-flat >& logs/log.beir-v1.0.0-cqadupstack-gis-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-mathematica-flat >& logs/log.beir-v1.0.0-cqadupstack-mathematica-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-physics-flat >& logs/log.beir-v1.0.0-cqadupstack-physics-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-programmers-flat >& logs/log.beir-v1.0.0-cqadupstack-programmers-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-stats-flat >& logs/log.beir-v1.0.0-cqadupstack-stats-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-tex-flat >& logs/log.beir-v1.0.0-cqadupstack-tex-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-unix-flat >& logs/log.beir-v1.0.0-cqadupstack-unix-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-webmasters-flat >& logs/log.beir-v1.0.0-cqadupstack-webmasters-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-wordpress-flat >& logs/log.beir-v1.0.0-cqadupstack-wordpress-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-quora-flat >& logs/log.beir-v1.0.0-quora-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-dbpedia-entity-flat >& logs/log.beir-v1.0.0-dbpedia-entity-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-scidocs-flat >& logs/log.beir-v1.0.0-scidocs-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-fever-flat >& logs/log.beir-v1.0.0-fever-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-climate-fever-flat >& logs/log.beir-v1.0.0-climate-fever-flat &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-scifact-flat >& logs/log.beir-v1.0.0-scifact-flat &

nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-trec-covid-multifield >& logs/log.beir-v1.0.0-trec-covid-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-bioasq-multifield >& logs/log.beir-v1.0.0-bioasq-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-nfcorpus-multifield >& logs/log.beir-v1.0.0-nfcorpus-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-nq-multifield >& logs/log.beir-v1.0.0-nq-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-hotpotqa-multifield >& logs/log.beir-v1.0.0-hotpotqa-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-fiqa-multifield >& logs/log.beir-v1.0.0-fiqa-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-signal1m-multifield >& logs/log.beir-v1.0.0-signal1m-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-trec-news-multifield >& logs/log.beir-v1.0.0-trec-news-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-robust04-multifield >& logs/log.beir-v1.0.0-robust04-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-arguana-multifield >& logs/log.beir-v1.0.0-arguana-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-webis-touche2020-multifield >& logs/log.beir-v1.0.0-webis-touche2020-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-android-multifield >& logs/log.beir-v1.0.0-cqadupstack-android-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-english-multifield >& logs/log.beir-v1.0.0-cqadupstack-english-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-gaming-multifield >& logs/log.beir-v1.0.0-cqadupstack-gaming-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-gis-multifield >& logs/log.beir-v1.0.0-cqadupstack-gis-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-mathematica-multifield >& logs/log.beir-v1.0.0-cqadupstack-mathematica-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-physics-multifield >& logs/log.beir-v1.0.0-cqadupstack-physics-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-programmers-multifield >& logs/log.beir-v1.0.0-cqadupstack-programmers-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-stats-multifield >& logs/log.beir-v1.0.0-cqadupstack-stats-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-tex-multifield >& logs/log.beir-v1.0.0-cqadupstack-tex-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-unix-multifield >& logs/log.beir-v1.0.0-cqadupstack-unix-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-webmasters-multifield >& logs/log.beir-v1.0.0-cqadupstack-webmasters-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-cqadupstack-wordpress-multifield >& logs/log.beir-v1.0.0-cqadupstack-wordpress-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-quora-multifield >& logs/log.beir-v1.0.0-quora-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-dbpedia-entity-multifield >& logs/log.beir-v1.0.0-dbpedia-entity-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-scidocs-multifield >& logs/log.beir-v1.0.0-scidocs-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-fever-multifield >& logs/log.beir-v1.0.0-fever-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-climate-fever-multifield >& logs/log.beir-v1.0.0-climate-fever-multifield &
nohup python src/main/python/run_regression.py --index --verify --search --regression beir-v1.0.0-scifact-multifield >& logs/log.beir-v1.0.0-scifact-multifield &
```

The `--regression` option specifies the regression to run, corresponding to the YAML configuration file in [`src/main/resources/regression/`](../src/main/resources/regression/).
The three main options are:

+ `--index`: Build the index.
+ `--verify`: Verify index statistics.
+ `--search`: Perform retrieval runs and verify effectiveness.

**Watch out!** The full `cw12` regression can take a couple days to run and generates a 12TB index!

Although the regression script is hard-coded to run on Waterloo machines (paths to corpoa are hard-coded), the corpus path can be manually specified from the command line with the `--corpus-path` option, for example:

```bash
python src/main/python/run_regression.py --index --verify --search --regression disk45 --corpus-path /path/to/corpus
```
