Content Brief
From scaling to over 100 million audio files to processing half a trillion events per day, Spotify’s infrastructure is built to serve millions of users seamlessly.
This is a look under the hood at Spotify’s engineering stack: from how they build their desktop and web apps to how they process petabytes of user data — all sourced from their official engineering blog and Google Cloud case study. 
This stack shows how Spotify balances global delivery, real-time data, and innovative user experiences — all while enabling rapid development across platforms.
#SpotifyEngineering #TechStack #CloudInfra #FrontendTech #DataEngineering
<other hashtags as appropriate>

Design Brief
Follow this template as it was a successful post and design.



Technology
Tag
Description
Source of info
Logo(s) to use
React + TypeScript
[Frontend]
Powers Spotify’s fast, modular UI
“overhaul … 2021” (Okoone)
React, Typescript
Chromium Embedded Framework (CEF)
[Desktop Runtime]
Renders Spotify’s desktop apps via a native shell, enabling rapid iteration using web technologies.
https://engineering.atspotify.com/2021/04/building-the-future-of-our-desktop-apps
https://github.com/chromiumembedded

Backstage
[Internal Tooling]
Spotify's open platform for building internal developer portals
(Spotify Engineering, InfoQ)
https://github.com/backstage/backstage

Java / Scala
[Backend]
Core backend services built in Java (Spring) and Scala for business logic and data processing.
(Okoone)
Java logo
Pub/Sub
[Streaming]
Handles Spotify’s event-driven architecture
https://cloud.google.com/customers/spotify
Google cloud logo
https://cloud.google.com/pubsub/docs/overview

BigQuery
[Data Warehouse]
Querying petabytes of audio, user, and event data to drive product decisions.
https://cloud.google.com/customers/spotify
Google cloud logo


Cloud Storage
[Storage]
Over 100 million audio files with globally distributed, durable access.
https://cloud.google.com/customers/spotify
Google cloud logo



Dataflow
[Data Processing]
Uses Apache Beam, crucial for personalizing audio experiences.
https://cloud.google.com/customers/spotify
Google cloud logo


Fleet Management + Kubernetes + GCP
[Infrastructure / CI‑CD]
Declarative infra with Kubernetes, GitOps-like flow, CRDs, and fleet automation
(Spotify Engineering, Data Integration, The New Stack)
Kubernetes logo https://kubernetes.io/ + Google Cloud Icon

Tingle (Build System)
[CI/CD]
Spotify’s internal build and CI/CD-like system using template-based YAML pipelines and GitHub webhook integrations.
(The New Stack)
Spotify logo https://github.com/spotify/luigi

Luigi (Workflow Orchestration)
[Data Processing]
Python-based task orchestration for distributed, make-like data workflows.
https://github.com/spotify/luigi
Spotify logo 
Fastly
[Streaming / Delivery]
CDN for fast, low-latency music streaming
https://engineering.atspotify.com/2020/02/how-spotify-aligned-cdn-services-for-a-lightning-fast-streaming-experience
https://www.fastly.com/products/cdn
