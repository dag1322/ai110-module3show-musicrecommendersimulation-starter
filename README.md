# 🎵 Music Recommender Simulation

## Project Summary

In this project you will build and explain a small music recommender system.

Your goal is to:

- Represent songs and a user "taste profile" as data
- Design a scoring rule that turns that data into recommendations
- Evaluate what your system gets right and wrong
- Reflect on how this mirrors real world AI recommenders

Replace this paragraph with your own summary of what your version does.

---

## How The System Works

Real-world music recommendation systems like Spotify or Apple Music analyze vast amounts of user data including listening history, explicit preferences, and behavioral patterns to suggest songs. They use complex algorithms combining collaborative filtering (what similar users like), content-based filtering (song attributes), and sometimes deep learning models to predict what you'll enjoy next. These systems prioritize personalization, discovery, and engagement while balancing factors like diversity, novelty, and avoiding filter bubbles.

My version will prioritize a simple content-based approach that matches user preferences directly to song attributes, focusing on musical "vibe" through genre, mood, and audio features. It will calculate relevance scores based on how well songs match a user's stated preferences, then rank and recommend the highest-scoring songs. This approach emphasizes transparency and interpretability over the black-box nature of large-scale systems.

**Song object features:**
- genre (categorical: pop, lofi, rock, etc.)
- mood (categorical: happy, chill, intense, etc.) 
- energy (numerical: 0-1 scale of intensity)
- valence (numerical: 0-1 scale of positivity/happiness)
- danceability (numerical: 0-1 scale of groove/dance potential)

**UserProfile object features:**
- preferred_genre (categorical preference)
- preferred_mood (categorical preference)
- preferred_energy (numerical target value 0-1)
- preferred_valence (numerical target value 0-1)
- preferred_danceability (numerical target value 0-1)

**Algorithm Recipe:**
For each song, calculate a total score using these rules:
- +2.0 points for exact genre match
- +1.0 point for exact mood match  
- Energy similarity: 1 - |user_target_energy - song_energy|
- Valence similarity: 1 - |user_target_valence - song_valence|
- Danceability similarity: 1 - |user_target_danceability - song_danceability|

Total score = genre_points + mood_points + energy_similarity + valence_similarity + danceability_similarity

Songs are then ranked by total score (highest first) to generate recommendations.

**Potential Biases:** This system might over-prioritize genre matches (worth 2 points) compared to mood (1 point), potentially ignoring great songs that match the user's mood but are in different genres. It could also create filter bubbles by consistently recommending similar songs, limiting exposure to diverse musical styles.

---

## Getting Started

### Setup

1. Create a virtual environment (optional but recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate      # Mac or Linux
   .venv\Scripts\activate         # Windows

2. Install dependencies

```bash
pip install -r requirements.txt
```

3. Run the app:

```bash
python -m src.main
```

### Running Tests

Run the starter tests with:

```bash
pytest
```

You can add more tests in `tests/test_recommender.py`.

---

## Experiments You Tried

Use this section to document the experiments you ran. For example:

- What happened when you changed the weight on genre from 2.0 to 0.5
- What happened when you added tempo or valence to the score
- How did your system behave for different types of users

---

## Limitations and Risks

Summarize some limitations of your recommender.

Examples:

- It only works on a tiny catalog
- It does not understand lyrics or language
- It might over favor one genre or mood

You will go deeper on this in your model card.

---

## Reflection

Read and complete `model_card.md`:

[**Model Card**](model_card.md)

Write 1 to 2 paragraphs here about what you learned:

- about how recommenders turn data into predictions
- about where bias or unfairness could show up in systems like this


---

## 7. `model_card_template.md`

Combines reflection and model card framing from the Module 3 guidance. :contentReference[oaicite:2]{index=2}  

```markdown
# 🎧 Model Card - Music Recommender Simulation

## 1. Model Name

Give your recommender a name, for example:

> VibeFinder 1.0

---

## 2. Intended Use

- What is this system trying to do
- Who is it for

Example:

> This model suggests 3 to 5 songs from a small catalog based on a user's preferred genre, mood, and energy level. It is for classroom exploration only, not for real users.

---

## 3. How It Works (Short Explanation)

Describe your scoring logic in plain language.

- What features of each song does it consider
- What information about the user does it use
- How does it turn those into a number

Try to avoid code in this section, treat it like an explanation to a non programmer.

---

## 4. Data

Describe your dataset.

- How many songs are in `data/songs.csv`
- Did you add or remove any songs
- What kinds of genres or moods are represented
- Whose taste does this data mostly reflect

---

## 5. Strengths

Where does your recommender work well

You can think about:
- Situations where the top results "felt right"
- Particular user profiles it served well
- Simplicity or transparency benefits

---

## 6. Limitations and Bias

Where does your recommender struggle

Some prompts:
- Does it ignore some genres or moods
- Does it treat all users as if they have the same taste shape
- Is it biased toward high energy or one genre by default
- How could this be unfair if used in a real product

---

## 7. Evaluation

How did you check your system

Examples:
- You tried multiple user profiles and wrote down whether the results matched your expectations
- You compared your simulation to what a real app like Spotify or YouTube tends to recommend
- You wrote tests for your scoring logic

You do not need a numeric metric, but if you used one, explain what it measures.

---

## 8. Future Work

If you had more time, how would you improve this recommender

Examples:

- Add support for multiple users and "group vibe" recommendations
- Balance diversity of songs instead of always picking the closest match
- Use more features, like tempo ranges or lyric themes

---

## 9. Personal Reflection

A few sentences about what you learned:

- What surprised you about how your system behaved
- How did building this change how you think about real music recommenders
- Where do you think human judgment still matters, even if the model seems "smart"

