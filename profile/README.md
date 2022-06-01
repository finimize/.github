# Finimize Engineering

👋 Welcome to Finimize's GitHub organisation! This doc explains the various repos we maintain, and how they fit into our business.

At a high level, we maintain a React Native mobile app 'Finimize' (=[`oban`](#oban)), which relies on a Django-based monolithic backend running across several replicas on Kubernetes (=[`chivas`](#chivas)). That backend repo in turn calls out to some more micro-ish services, such as the financial data service which is spread across the several `com.finimize.financial-data.` repos.

Separately, we have a web app subscriptions.finimize.com backed by a React app and an Express server (both in [`lagavulin`](#lagavulin)). [Off GitHub](https://www.notion.so/5a8add9ccecf4a68bbd6ca6404b533a5), there is also the 'main' Finimize website, backed by a crusty old PHP repo that we don't need to change very often.

# Onboarding

Clone `chivas`, `lagavulin`, and `oban`. Put them somewhere sensible, like `~/src/github.com/finimize` - up to you. If you were given onboarding instructions, do those; if you weren't, then either (a) something went wrong or else (b) you are reading this from the year 3112 where all these problems have been solved automatically. Choose the option appropriate to you, and act accordingly.

- You're hopefully already on Slack. The `#eng` and `#core-eng` channels are the loci of engineering discussions, with the latter being a bit more 'internal'. Check your Gmail occasionally as well!

- No one is in charge. If you think something needs to be done, do it! Like, seriously, do. We'll actually review it. This is not a trap.

- You'll occasionally be asked to provide time estimates for tickets. Remember to factor in important professional duties like planning, testing, and browsing HN.

# Codebases

## `chivas`

This is our Django monolith, which we run as a set of pods (`chivas-web`) on our staging and production Kubernetes clusters.

When we merge a change into `master`, a [CI job](https://app.circleci.com/pipelines/github/finimize/chivas) deploys it automatically to staging, and deploys it to production when you click the thumbs-up button under `hold_server`. (You don't have to, but we _try_ not to let production get too far out of sync.)

👉 [Docs](https://github.com/finimize/chivas/wiki)

## `oban`

This is the mobile app, written in React Native with a smattering of native (i.e. ObjC & Java).

We practise discontinuous deployment from `master`: a [CI job](https://app.circleci.com/pipelines/github/finimize/oban) will run the build and tests, and clicking the go-ahead button under `hold_for_testflight` will kick off a TestFlight build. This can be done for non-`master` builds too. If the Oban docs linked below don't help, check with me (Sam R-A) or Matt D.

👉 [Docs](https://github.com/finimize/oban/wiki)

## 'FinData' repos

This section covers the repos named like `com.finimize.financial-data.*`. These are 'polyrepos' jointly implementing our financial data service, which collects stock pricing data from multiple sources, carrying out some ETL-like tidy-up functions, and then serving it over an API to the backend proper (`chivas` above).

👉 [Docs](/dev/null)
