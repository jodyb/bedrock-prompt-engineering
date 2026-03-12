# Bedrock Prompt Engineering

Prompt engineering techniques and evaluation frameworks for Amazon Bedrock, applied to P&C insurance use cases.

## Overview

This project demonstrates a systematic progression from basic prompting through production-ready multi-task architectures. All examples use real-world Property & Casualty insurance scenarios — claim classification, fraud detection, coverage determination, and policyholder communication.

**Model:** Claude Sonnet 4.5 via Amazon Bedrock Converse API
**Region:** us-east-1
**Runtime:** SageMaker Studio / Jupyter

## Notebooks

| # | Notebook | Focus |
|---|---------|-------|
| 01 | `01-prompt-fundamentals.ipynb` | Zero-shot, few-shot, role-based, and structured output techniques. Side-by-side comparison on the same claims. |
| 02 | `02-chain-of-thought.ipynb` | Chain-of-thought reasoning — standard CoT, step-by-step decomposition, and self-consistency for complex claim analysis. |
| 03 | `03-structured-extraction.ipynb` | JSON schema-driven extraction, handling missing/ambiguous data, and parse validation for downstream pipelines. |
| 04 | `04-system-prompts.ipynb` | Progressive system prompt layering (persona → scope → guardrails), composable prompt architecture (4×4×3 = 48 configurations from 11 blocks), and guardrail boundary testing. |
| 05 | `05-prompt-templates.ipynb` | F-strings → string.Template → PromptTemplate class. Template libraries, conditional templates, and multi-step claim pipelines. |
| 06 | `06-evaluation-framework.ipynb` | Three-tier evaluation pyramid: rule-based (100% of responses), LLM-as-judge (10%), and human review (1%). Combined scoring with weighted dimensions. |
| 07 | `07-red-teaming.ipynb` | Adversarial testing suite — prompt injection, jailbreak attempts, guardrail bypass. Automated scoring, defense strategies, and hardened system prompts. |
| 08 | `08-prompt-optimization.ipynb` | A/B testing framework for prompt variants. Token efficiency analysis, cost projections, quality vs. cost tradeoffs, and complexity-based routing. |
| 09 | `09-multi-task-architecture.ipynb` | Task registry, dispatcher, and pipeline orchestration with shared context. Multiple pipeline configurations (standard, fast triage, fraud-focused) with production cost analysis. |

## Key Concepts

**Prompt Architecture:** System prompts are composed from reusable building blocks — persona (who), scope (what), and guardrails (how). This composable approach produces consistent, auditable prompt configurations.

**Evaluation:** Quality is measured through a three-tier pyramid. Rule-based checks catch structural failures fast and free. LLM-as-judge evaluates reasoning depth on a sample. Human review validates the final production configuration.

**Optimization:** Prompt variants are tested A/B style against the same claims, measuring quality, token cost, and latency. Output tokens cost 5× more than input tokens — structured output formats (JSON) can significantly reduce cost while maintaining quality.

**Security:** Red teaming covers prompt injection, jailbreak attempts, and guardrail bypass. Defense is layered: model training (Layer 1), system prompt guardrails (Layer 2), and infrastructure enforcement via Bedrock Guardrails (Layer 3).

**Multi-Task Architecture:** Claims processing is decomposed into discrete tasks (classify, severity, fraud screen, coverage, communicate), each with its own optimized prompt. A dispatcher routes claims through predefined pipelines with shared context flowing between tasks. This architecture is the foundation for agent-based systems.

## Prerequisites

- AWS account with Amazon Bedrock access (Claude Sonnet 4.5 enabled in us-east-1)
- SageMaker Studio or Jupyter environment with `boto3`
- IAM role with `bedrock:InvokeModel` permissions

## Cost

Running all notebooks end-to-end costs approximately $1–3 in Bedrock API charges, depending on model pricing at time of execution.

## Related Projects

- [sagemaker-policyholder-lapse-prediction](https://github.com/jodyb/sagemaker-policyholder-lapse-prediction) — Phase 1: ML foundations with SageMaker (XGBoost, feature engineering, model deployment)
- [bedrock-insurance-ai](https://github.com/jodyb/bedrock-insurance-ai) — Phase 2: Bedrock fundamentals (model selection, inference parameters, multi-modal)

## License

MIT