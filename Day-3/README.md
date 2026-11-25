# LLM Multi-Provider Evaluation & Chat Agent Project

This notebook demonstrates how to set up, query, and evaluate three prominent Large Language Model (LLM) API providers using **LangChain**: **Groq**, **OpenAI**, and **Google Gemini**.

---

## 📋 Project Structure & Usage

### 1. Sweet Crumbs Home Bakery Agent
* **Purpose**: Simulates a friendly assistant managing customer cake queries with strict business rules.
* **Key Code**: Uses `ChatGroq` coupled with custom system instructions to parse user questions, remember customer names (`history`), and ensure correct pricing and capabilities are relayed.
* **Test Suite**: Includes an automated check (`run_tests()`) using a simple CSV template (`/content/test.csv`) to verify exact key-phrase presence like "yes", "500", and "owner".

### 2. Sparkle Clean Car Wash Evaluator
* **Purpose**: Simulates a car wash assistant providing answers about wash tiers, eco-friendly configurations, and booking protocols.
* **Evaluation Engine**: Features a parameterized runner function `evaluate_model` executing 10 testing queries from `/content/custom_tests.csv` and reporting pass/fail scores.

---

## 📊 API Comparison & Performance Summary

| Provider | Default Model Checked | Performance Notes & Error Profiles |
| :--- | :--- | :--- |
| **Groq** | `openai/gpt-oss-120b` | **Excellent & Highly Stable**: Handled all 10 tests with 80% baseline compliance and zero rate-limiting/token quota blocks. |
| **OpenAI** | `gpt-4o-mini` | **Quota Restricted**: Halted execution with a **429 (credit_balance_exhausted)** error because there were insufficient credits on the target account. |
| **Google Gemini**| `gemini-3.5-flash` | **Rate Limited on Free Tier**: Easily hit a **429 RESOURCE_EXHAUSTED** error because the free tier enforces a strict 5 requests-per-minute (RPM) ceiling. |

---

## 🌡️ Optimal Temperature Setting

### Which temperature works perfectly?
* **`temperature = 0.3` (Recommended)**: Best suited for system tasks, enterprise compliance, and structured data-matching checks (such as the `must_include` test validations). It ensures low variance, high determinism, and highly repeatable responses.
* **`temperature = 1.0` (High Variance)**: Triggers creative variation, which can degrade strict assertion checks. Minor phrase variations cause evaluations to fail intermittently even when the core facts are technically present.
