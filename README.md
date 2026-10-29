# Europe MOI Scholarship Finder

A structured LLM prompt for finding funded Master's scholarships in Europe that accept a **Medium of Instruction (MOI) certificate** instead of IELTS/TOEFL. Built for Bangladeshi applicants in Computer Science / IT, and easy to adapt to other profiles.

## What this does

Most scholarship lists ignore the MOI question, which is the main filter for applicants without IELTS/TOEFL. This prompt forces the LLM to:

- Filter by an application deadline window (default: Nov 1, 2026 to Jan 31, 2027)
- Check MOI acceptance per university and per program, not just per country
- Return a single table with 13 columns, including separate columns for the scholarship page and the university application portal
- Mark anything it cannot verify as `Not verified` instead of inventing links or dates
- List excluded scholarships with reasons, so you can see what was filtered out

## How to use

1. Open an LLM **with live web search enabled** (without it, deadlines and links will be stale or wrong).
2. Copy the prompt from the section below.
3. Replace `[YOUR SUBJECT]` with your bachelor's subject. Edit nationality, CGPA, and field if your profile differs.
4. Paste it and run it.
5. **Verify every deadline, link, and MOI rule on the official website** before applying.

## The prompt

```
ROLE
You are a research assistant specializing in international graduate admissions and scholarships in Europe.

TASK
Build a verified list of fully or partially funded Master's scholarships at European universities whose application deadlines fall between November 1, 2026 and January 31, 2027 (today is October 28, 2026). Include only scholarships at universities that accept a Medium of Instruction (MOI) certificate in place of IELTS/TOEFL for Bangladeshi applicants.

APPLICANT PROFILE
- Nationality: Bangladeshi
- Bachelor's degree: BSc in [YOUR SUBJECT], Bangladesh, CGPA 3.62/4.00
- Intended Master's field: Computer Science or any related IT field (e.g., Data Science, AI, Software Engineering, Cybersecurity, Information Systems)
- Language of instruction: English
- Proof of English: MOI certificate only (no IELTS/TOEFL, and no plan to take them)

SCOPE
- Countries: EU/EEA countries plus the UK, Switzerland, and other European countries
- Level: Master's only
- Include both university-specific scholarships and government or consortium scholarships (e.g., Erasmus Mundus), if the deadline fits and the program accepts MOI.

REQUIRED COLUMNS
1. Scholarship name
2. University name
3. Country
4. Application opening date
5. Application deadline
6. Program start date (intake)
7. Funding type (full / partial / tuition waiver; monthly stipend if any)
8. MOI acceptance: Yes / Conditional / Unconfirmed, with the specific condition (e.g., bachelor's must be taught entirely in English, certificate wording requirements, whether Bangladeshi MOI is accepted)
9. Eligibility notes for Bangladeshi applicants (minimum CGPA, work experience, age limit, etc.)
10. Required documents
11. Official scholarship page link
12. Official university admissions/application portal link (separate column)
13. Source and date you last verified the information

You may add useful columns (e.g., application fee, separate scholarship application required, program name).

RULES
- Use only official university or government websites as sources.
- Never invent or guess a link, deadline, or MOI policy. If you cannot verify a field, write "Not verified".
- If the 2026-27 deadline is not confirmed, write "Check official site" and do not guess a date.
- Exclude any scholarship or program that requires IELTS/TOEFL with no MOI alternative.
- Sort by deadline, earliest first.
- At the end, list the scholarships you considered but excluded, with the reason for each.

OUTPUT FORMAT
A single table that I can copy into a Word or Google Docs file. If you can create a document file directly, do that. Otherwise give a CSV.
```

## Customizing

| To change | Edit this part |
|---|---|
| Different nationality | `Nationality` line, plus every "Bangladeshi" in the TASK and column 9 |
| Different field | `Intended Master's field` line |
| Different deadline window | Dates in the TASK section, and "today is ..." |
| Specific countries only | `Countries` line under SCOPE |
| Different English proof | `Proof of English` line, and the exclusion rule under RULES |

## Known limitations

- **The list will likely be short.** Many European universities do not accept MOI from Bangladesh and require IELTS/TOEFL. A short list means the filter is working. A long list of fully "verified" rows is a warning sign of fabricated entries.
- **MOI policy is decided by the university or program**, not the scholarship. Always confirm with the admissions office in writing.
- **LLMs can still hallucinate links and dates**, even with rules against it. Open every link yourself.
- **Deadlines change every year.** Re-run the prompt with updated dates each admission cycle.

## Second prompt: Single Scholarship Fact-Checker

Use this when you already have a specific scholarship (a name, a link, or a flyer) and want its full details checked against official sources. The first prompt *finds* scholarships. This one *verifies* one.

### What this does

- Finds the official scholarship page and application portal, and checks the scholarship really exists there
- Tells you whether applications are open, closed, or not yet open, and for which intake
- Breaks the scholarship into Eligibility, Benefits, Application Process, and Deadline, using exact figures
- Compares any flyer or blog figures against the official page and lists every mismatch
- Warns about hidden traps (funding not guaranteed, unaccepted tests, paid prep years)
- Marks anything it cannot confirm as `not verified`

### How to use

1. Open an LLM **with live web search enabled**.
2. Copy the prompt below.
3. Replace `[SCHOLARSHIP NAME OR LINK]` with the scholarship name or the link or flyer you found.
4. Optionally fill in the last line (`[YOUR COUNTRY, DEGREE, FIELD, LANGUAGE TEST/SCORES]`) so the answer can tell you whether you qualify, not just what the rules are.
5. Confirm the final deadline by email with the official contact before you pay or travel.

### The prompt

```
Research this scholarship: [SCHOLARSHIP NAME OR LINK]

Use only OFFICIAL sources (the university's or the funding organization's own website). Treat scholarship blogs and aggregator sites as unreliable. Use them only to find the scholarship's name, never as proof of a fact.

Do this:
1. Find the official application portal link and the official scholarship page. If a link was given, check whether the scholarship really exists on the official site.
2. Check today's date and tell me whether applications are open, closed, or not yet open. Name the exact intake (for example Fall 2027 or Spring 2027) that each deadline applies to.
3. Give me these sections, with exact numbers from the official page:
   - Eligibility Criteria: degree level, who can apply, GPA, nationality limits, language tests with minimum scores, entrance exams (GRE, GMAT, etc.), age limits, and which language certificates are NOT accepted
   - Benefits: tuition, monthly stipend (exact amount and number of months), housing, health insurance, travel, other perks, and whether funding is guaranteed or only possible
   - Application Process: step-by-step, required documents, recommendation letters (who and how they are submitted), application fee, interviews
   - Deadline: exact dates, early deadlines, interview dates, and the date my previous degree must be finished
4. Compare any figures in the link or flyer I gave against the official page. List every mismatch (deadline, amounts, levels, years).
5. Warn me about hidden traps, such as scholarships that aren't guaranteed on admission, tests that aren't accepted, extra paid prep years, or documents that take a long time to get.
6. If something can't be confirmed from an official source, say "not verified" instead of guessing.
7. End with a list of sources (official links only) and an official contact email or phone number I can use to confirm details.

Be direct. Don't praise the scholarship. If it looks like a scam, outdated, or misleading, say so in the first line.

My situation (optional): [YOUR COUNTRY, DEGREE, FIELD, LANGUAGE TEST/SCORES]
```

### Tips

- If the scholarship has no official link yet, ask the LLM for the university's admissions page first, then the scholarship page.
- Scholarship blogs often copy old amounts and deadlines. If the answer lists mismatches, trust the official page.
- A scholarship page can apply to one intake or one program only. Check that the deadline matches the intake you want.

## Disclaimer

This repository contains prompt templates only. It does not contain scholarship data, and nothing here is official admissions or legal advice. Always rely on official university and government sources.

## License

MIT
