# Self Introduction

Hi, my name is **Xayrulloh**. I’m a **full-stack developer** with around **5 years of experience**, mainly working with **Node.js, React, and PostgreSQL**, along with modern frameworks and libraries in the JavaScript ecosystem.

On the cloud side, I’ve worked with **AWS, Google Cloud Platform, and Cloudflare**, deploying and maintaining production systems, including containerized and serverless solutions.

Throughout my career, I’ve been involved in projects across different domains such as **e-commerce, logistics, social platforms, and AI-driven products**, usually working on both backend architecture and frontend integration.

One project I’d like to highlight is a **Customer Feedback Sentiment Dashboard** that I built recently. The goal was to simplify how companies work with user feedback and reports. Users submit feedback, and the system uses AI to automatically **analyze sentiment**—positive, negative, or neutral—generate metrics, and present them in a **clear and simple UI**.

Additionally, reports are **grouped and summarized**, making it easier for teams to understand recurring issues. If documentation is provided, the system can also **answer user questions using RAG**, which significantly reduces the need for manual support and human resources. The project was designed with scalability and real business use cases in mind.

Besides commercial work, I also build **my own products**. Some of them have grown into **early-stage startups**, and a few already have **thousands of users**, which gave me strong experience in product thinking, performance optimization, and real-world scalability.

That’s a quick overview of my background. I’d be happy to go deeper into any part or answer any questions you have.


# Behavioral Interview Questions

1. ## **Tell me about the most difficult bug you’ve fixed.**

   _There was one slow, hard-to-understand SQL query with several subqueries.
   They wanted me to fix it, make it easier to understand, and optimize it. In
   the beginning, it was hard to follow, so I started analyzing the query by
   splitting it into pieces. Once I understood it fully, I began optimizing it
   by using the WITH keyword to create temporary tables inside the query. This
   really helped remove unnecessary subqueries. In the end, I achieved a clean,
   easy-to-read query that was also faster, improving the API response time._

2. ## **Describe a challenging programming problem you faced and how you resolved it.**

   _When I worked on the Shichu project (Japan), there was a feature where voice
   actors could give their voices to characters, and users could choose
   different/multiple voices. We used ffmpeg in our service, which is
   CPU-intensive, and it caused our API to slow down or sometimes not respond.
   My first solution was to avoid blocking the main thread — I moved the ffmpeg
   processing into Worker Threads. That helped for a while, but as API calls
   increased, we needed more worker capacity. Instead of just scaling threads, I
   moved the ffmpeg part to a GCP Cloud Run service. The main reason was easy
   scaling — when requests increase, GCP scales automatically. Another reason
   was cost — the team decided GCP was cheaper than AWS for our case, and since
   we were already using Google Cloud Storage, it was easier to pull the audio
   files directly. (Yes, we could’ve used AWS Lambda + S3, but the choice was
   already made.)_

3. ## **Imagine you have been accepted into the team. What would be your first course of actions?**

   _First of all, I would try to understand the product that we’re dealing with;
   **not just the general info, but the true essence of the product and what
   kind of problem we’re trying to tackle. I firmly believe that I will be able
   to contribute more to the project if I have a very good understanding of it.
   To make sure I have a clear picture and vision of the project, I would try to
   talk with some members of the team and ask them all sorts of questions
   regarding the project**. Once I have a very grasp of the project, I believe I
   will be ready to start my tickets and contribute to the project._

4. ## **Describe a time when you had to make a difficult decision based on incomplete information.**

   _Estimating tasks without full information is always tricky because it can
   lead to unexpected problems and sleepless nights. That’s why I always try to
   clarify requirements before starting, or at least warn the team if something
   is unclear so everyone is aware of the risks._

5. ## **Tell me about a time you had a disagreement with a manager or coworker. How did you handle it?**

   _Our PM introduced a new rule: if someone won’t finish their task on time,
   nobody could leave the office until it was done — everyone had to help. I
   disagreed because this punished people who completed their work on time, and
   could cause resentment. After discussing it, we changed the rule so that if
   someone won’t finish by Friday, they would work on the weekend instead. This
   was a fairer approach._

6. ## **Describe a situation where you had to work closely with someone whose personality was very different from yours.**

   _I honestly haven’t had that happen yet. But my approach is always to stay
   friendly and try to understand the other person rather than argue. If I need
   to disagree, I prefer doing it privately — either in chat or one-on-one —
   instead of in public, because public arguments can make someone feel
   embarrassed or defensive. I collect my evidence and share it calmly so he/she
   can understand my point._

7. ## **Give an example of a time you had to persuade someone at work to see things your way.**

   _I don’t usually like “persuading” just for the sake of it — maybe my way
   isn’t the best. Instead, I try to compare both sides and see which one works
   better. If my way is clearly better, I explain it logically and let the
   results speak for themselves._

8. ## **How do you ensure effective communication with remote team members?**

   _Rule number one: don’t disturb them unnecessarily. Rule number two: don’t
   ask questions without trying to find the answer yourself first. I only
   message when it’s truly important, so they know I’m not just sending random
   or low-priority messages._

9. ## **Tell me about a recent failure and what you learned from the experience.**

   _When I was designing the database for my Family Tree project, I initially
   used a recursive SQL query for nested trees (father → son → grandson, etc.).
   But I realized it didn’t work for real-world cases — your spouse’s tree might
   be bigger than yours, so the tree grows both vertically and horizontally.
   That’s when I learned about graph databases. I redesigned the schema using a
   node-based approach, with two types of relationships: parent for vertical
   growth and spouse for horizontal growth._

10. ## **Tell me about a time when you had to learn a new technology quickly.**

    _When we switched to NestJS, I had to learn it fast. I read all the official
    documentation, explored open-source projects on GitHub, and read Medium
    articles. That’s my general learning process — I start with official docs
    but also look for third-party resources that might explain things more
    clearly._

11. ## **Describe a time when you went above and beyond the requirements for a project.**

    _This hasn’t happened to me yet, and honestly, I hope it won’t — because it
    often means the original requirements were underestimated or unclear._

12. ## **Where do you see yourself in five years?**

    _I usually plan short-term — daily, weekly, monthly, and yearly — but not
    much further. If I had to guess, maybe I’ll be a software engineer who can
    build not only web apps but also mobile, desktop, or other IT-related
    solutions._

13. ## **Describe a time when your team or company was undergoing some change. How did you adapt?**

    _In one project, we were using NX with nx/webpack, but over time we realized
    nx/webpack wasn’t a good choice. We switched to Rspack. It took a day to
    migrate the whole codebase, and although Rspack’s config is similar to
    Webpack’s, we still faced some compatibility issues. In the end, the
    migration improved build times and overall developer experience._

14. ## **What aspects of your work are most often criticized? How have you handled criticism of your work?**

    _Early in my career, I had a habit of thinking too much about future
    features for a project that hadn’t even started. While it’s good to plan
    ahead, overthinking future work can hurt focus on current tasks. Now I only
    think about upcoming features when it’s actually necessary — otherwise, I
    stay fully focused on what I’m doing now._

15. ## **Imagine you’re a team lead and you have a conflict with one of your team members. You think a certain feature should be developed, while your team member thinks it shouldn’t exist. How would you resolve this conflict?**

    _Based on my experience as a team lead, the way one resolves such conflicts
    is by **gathering everyone in the room and just talking it through,
    regardless of whether it takes a few minutes or a few hours. It is very
    important to keep in mind that you have to stay open to listen to and
    consider the arguments of your team member throughout the entire
    discussion**, while also presenting your own arguments. You typically end up
    being able to resolve the conflict and find a common ground with your
    teammates. While such approach might seem time-consuming, it pays off later
    since that team member will not feel like they aren’t part of the team and
    that their opinion isn’t valued._
