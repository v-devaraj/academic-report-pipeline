# Build Log: AI-Assisted Academic Data Report Pipeline

Honest record of building this project: written at the time, not reconstructed later.

---

## 1. Time measurements (manual vs. pipeline)

**Fairness rules:** same input file, same output format, same quality bar;
pipeline time includes my review of AI output; build time reported separately;
any extrapolation is stated.

| Date | Task | Manual (min) | Pipeline (min, incl. review) | Notes |
|------|------|--------------|------------------------------|-------|
|      |      |              |                              |       |

**Build time so far:**
- Phase 0 (setup): 3 hours, 2026-11-15

---

## 2. Problems and how I solved them

### 2026-11-15 | API key length didn't match the expected format
- **Problem:** loaded key was 53 characters; I expected ~39 (`AIza...` format).
- **Investigation:** checked Google's documentation instead of assuming the key was broken.
- **Cause:** since mid-2026, AI Studio issues new `AQ.`-format keys, which are longer.
- **Verification:** confirmed prefix and no spaces with a Python check, without printing the key.
- **Decision:** use Google's native Gemini SDK (some third-party/OpenAI-compatible routes reject `AQ.` keys).

### 2026-11-15 | First `git push` failed with an authentication error
- **Problem:** "Invalid username or token. Password authentication is not supported."
- **Cause:** Windows had a stale saved GitHub credential, which Git reused automatically.
- **Fix:** the failed attempt cleared it; retrying triggered browser sign-in and saved a new token.
- **Lesson:** I first thought an unrelated command (`git branch -M main`) fixed it. I checked: it
  couldn't have, since the branch was already `main`. Read the error; change one thing at a time.

---

## 3. Prompt versions and what improved

| Version | Date | What changed | Result |
|---------|------|--------------|--------|
|         |      |              |        |

---

## 4. Tools integrated and why

| Tool | Purpose | Why this one |
|------|---------|--------------|
| Python + `venv` | Isolated project environment | Built-in, no extra install; reproducible via `requirements.txt` |
| `python-dotenv` + `.env` | Keep API key out of code | Standard practice; `.gitignore` prevents leaks |
| Git + GitHub | Version history, backup, portfolio | Tracks prompt/code changes as evidence |
| Google Gemini API (free tier) | LLM diagnosis step | $0, no card needed, easy from India |

---

## 5. Decisions and trade-offs

- **2026-11-15 | venv over uv/conda:** fewest new concepts; uv is a later upgrade.
- **2026-11-15 | Gemini free tier over Claude/OpenAI:** no card; per-run cost would be under
  1 cent on paid models anyway, so card requirement and data terms mattered more than price.
- **2026-11-15 | Flash vs Flash-Lite not decided yet:** will test both on the same students
  and record the comparison (section 3).
- **2026-11-15 | Synthetic data only:** free-tier inputs may be used by Google to improve
  its products; with real student data I'd use a paid tier with no-training terms,
  send only de-identified fields, and get data-owner sign-off.
- **2026-11-15 | Rules before LLM:** rules cheaply narrow ~500 students to ~30; smaller,
  per-student LLM calls are cheaper, within rate limits, and more reliable.