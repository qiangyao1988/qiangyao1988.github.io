---
permalink: /
title: ""
excerpt: ""
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='about-me'></span>

I am currently in the fifth year of my Ph.D. program in the Department of Computer Science at Wayne State University, 
where I work in the Trustworthy AI lab under the supervision of <a href="https://dongxiaozhu.github.io/" target="_blank"> Dr. Dongxiao Zhu</a>. 
My research mainly focuses on Natural Language Processing (NLP)&Large Language Models (LLMs), Trustworthy Artificial Intelligence (AI), and Machine Learning Theory & Applications. 
My dedication to these areas has led to the publication of numerous research papers at top AI conferences, including NeurIPS, IJCAI, AAAI, ICML, MICCAI, and IJCNN, among others. 
I have a strong passion for research and a demonstrated ability to apply my knowledge to real-world challenges.

# 🔥 News
- *2023.10*: &nbsp;✨ New [preprint](https://arxiv.org/abs/2310.06387) on **LLM Safety** is available at arxiv.
- *2023.09*: &nbsp;🎖 I won the **Award for Academic Innovation** in the academic year 2022-2023 (**only 1 awardee** among undergraduates in School of Mathematical Sciences, Peking University, **Top 0.1%**).
- *2023.08*: &nbsp;🎉 1 Paper (as first author) accepted by **Journal of Logical and Algebraic Methods in Programming**.
- *2023.08*: &nbsp;🏫 I started a visiting student program at **UC Berkeley** in Fall 2023.
- *2023.07*: &nbsp;🏖 I attended **ICML 2023** at Honolulu and illustrated our workshop poster.
- *2023.07*: &nbsp;🔍 I reviewed 11 papers for **NeurIPS 2023** (9 regular + 2 ethics).
- *2023.06*: &nbsp;🎉 1 Paper (as first author & corresponding author) accepted by **ICML 2023 AdvML-Frontiers Workshop**.
- *2023.06*: &nbsp;🍁 I attended **CVPR 2023** at Vancouver and illustrated our poster.
- *2023.05*: &nbsp;🥈 Won **Second prize** in Chinese Mathematics Competitions for College Students **(National final)**.
- *2023.05*: &nbsp;🎙 I gave a talk on our CVPR paper in **Safe & Responsible AI workshop** (ICLR 2023 social event) at Tsinghua University.
- *2023.02*: &nbsp;🎉 1 Paper (as first author) accepted by **CVPR 2023**.
- *2022.12*: &nbsp;🥇 Won **First prize** in Chinese Mathematics Competitions for College Students (Beijing Division), and qualified for the finals.

# 📝 Selected Papers

## Jailbreak and Guard Aligned Language Models with Only Few In-Context Demonstrations (Preprint)
**Zeming Wei**, Yifei Wang, Yisen Wang${}^\dagger$
- Uncover the vulnerability and robustness of aligned language models under only few in-context demonstrations without fine-tuning
- Propose In-Context Attack (ICA) and In-Context Defense (ICD) to jailbreak and guard aligned language models
- Shed light on the potential of in-context learning (ICL) to manipulate the alignment of LLMs
- [[pdf](https://arxiv.org/pdf/2310.06387)] [[arxiv](https://arxiv.org/abs/2310.06387)]

## CFA: Class-wise Calibrated Fair Adversarial Training (CVPR 2023)
**Zeming Wei**, Yifei Wang, Yiwen Guo, Yisen Wang${}^\dagger$
- Theoretically and empirically investigate the preference of different classes for adversarial configurations in Adversarial Training (AT)
- Propose a CFA framework that customizes specific training configurations for each class automatically
- CFA improves both overall robustness and fairness, and can be easily incorporated into other AT variants
- [[pdf](https://openaccess.thecvf.com/content/CVPR2023/papers/Wei_CFA_Class-Wise_Calibrated_Fair_Adversarial_Training_CVPR_2023_paper.pdf)] [[arxiv](https://arxiv.org/abs/2303.14460)] [[code](https://github.com/PKU-ML/CFA)]

## Sharpness-Aware Minimization Alone can Improve Adversarial Robustness (ICML 2023 Workshop)
**Zeming Wei\*${}^{\boldsymbol\dagger}$**, Jingyu Zhu\*, Yihao Zhang\*
- Theoretically show that using Sharpness-Aware Minimization (SAM) can improve adversarial robustness
- Empirically illustrate that SAM can improve robustness with a friendly computational cost and no decrease in natural accuracy
- Propose that SAM can be regarded as a lightweight substitute for AT under certain requirements
- [[pdf](https://arxiv.org/pdf/2305.05392)] [[arxiv](https://arxiv.org/abs/2305.05392)] [[code](https://github.com/weizeming/SAM_AT)]

## Weighted Automata Extraction and Explanation of Recurrent Neural Networks for Natural Language Tasks (Journal of Logical and Algebraic Methods in Programming)
**Zeming Wei**, Xiyue Zhang, Yihao Zhang, Meng Sun${}^\dagger$
- Extending WFA extraction methods of RNNs from formal to natural language tasks by identifying transition sparsity and context dependency problems
- Propose an RNN interpretation framework with a transition-based word embedding of the extracted automata  
- Further propose two applications (pretraining and adversarial attack) on RNNs with the embedding
- [[pdf](https://arxiv.org/pdf/2306.14040)] [[arxiv](https://arxiv.org/abs/2306.14040)] [[code](https://github.com/weizeming/Extract_WFA_from_RNN_for_NL)]

# 🎖 Honors and Awards
- **Michael E. Conrad Award (Highest Honor at WSU CS Department)**, *2023*
- **AAAI 2023 Student Scholarship**, *2022*
- **NeurIPS 2022 Scholar Award**, *2022*
- **Department Travel Award for Outstanding Conference Publications**, *2022*
- **Graduate Student Professional Travel Award**, *2022*
- **IEEE CIS Conference Participation and Travel Grants**, *2022*
- **IJCAI 2022 Travel and Accessibility Grant**, *2022*
- **Department Oustanding GTA Award**, *2020*
- **Graduate School Master’s Scholarship Award**, *2019*


# 📖 Educations
- *2019.09 - 2024.05 (expected)*, Doctor of Philosophy in Computer Science, Wayne State University
- *2018.09 - 2019.12*, Master of Science in Computer Science, Wayne State University
- *2006.09 - 2010.07*, Bachelor of Science in Computer Science, Wayne State University

# 💼 Academic Service
- **Program Committee Member**: SDM 2023, KDD 2023, AAAI 2022-2023, ICML 2022-2023
- **Journal Reviewer**: TKDD 2023, AI 2022, TIOT 2021
- **Conference Reviewer**: SDM 2023, KDD 2023, CVPR 2023, AAAI 2020-2023, NeurIPS 2020-2023, ICLR 2022-2023, IJCAI 2021-2023, MICCAI 2022-2023, ICML 2022-2023
- **Conference Student Volunteering**, AAAI 2023, NeurIPS 2022, IJCAI 2022, IJCNN 2022

# 🔗 Links
(Alphabetical Order)
- 👨‍🏫 **Advisors**: [Dongxiao Zhu](https://dongxiaozhu.github.io/)
- 🧑‍🎓 **Co-authors**: [Marco Brocanelli](),[Chengyi Li](), [Xin Li](), [Prashant Khanduri](), [Deng Pan]()
- 💻**Lab**: [Trustworthy Lab](https://sites.google.com/view/mlpa/mainpage)