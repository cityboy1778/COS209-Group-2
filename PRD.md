# Product Requirements Document
## Babcock Skill Swap

**Author:** Oluwapelumi Emmanuel Killa
**Version:** 1.0
**Date:** 22 November 2026

## 1. Overview
Babcock Skill Swap is an app where students trade skills with students from other courses, with no money. For example, a Computer Science student teaches coding, and a Mass Communication student teaches video editing.

## 2. Problem
Students have useful skills, but they only meet people in their own course. Paid classes and tutors are costly, so many students cannot learn new skills like design, public speaking, or coding. There is no easy way to find someone who wants what you know and knows what you want.

## 3. Goals
- Help students find a swap partner in under 2 minutes.
- Let students learn a new skill at no cost.
- Connect students across different courses.
- Make swaps safe and trusted.

**Not in scope (v1):** payments, people outside Babcock, and video calls.

## 4. Users
| User | Need |
|---|---|
| Student | List skills, find matches, chat, and swap |
| Admin | Remove bad users and handle reports |

## 5. User Stories
- As a student, I want to list what I can teach and what I want to learn, so the app can find me a match.
- As a student, I want to chat with my match, so we can agree on a time and place.
- As a student, I want to rate my partner after a swap, so others can trust them.
- As a student, I want to report a bad user, so I stay safe.

## 6. Key Features
1. **Sign up** with Babcock email or matric number
2. **Profile** with skills to teach and skills to learn
3. **Matching** that pairs students who want each other's skills
4. **Chat** between matched students
5. **Swap request** with accept or decline
6. **Ratings and reviews** after each swap
7. **Block and report** buttons
8. **Admin panel** to review reports

## 7. Requirements
**Functional**
- A student must add at least one teach skill and one learn skill.
- Only Babcock students can join.
- A student can only chat with people they matched with.
- Reviews can only be left after a completed swap.

**Non-functional**
- Pages load in under 3 seconds.
- Passwords and personal data are stored safely.
- Works on phones and small screens.

## 8. Success Metrics
- 500 students sign up in the first semester.
- 60% of users get at least one match.
- 40% of matches become a completed swap.
- Average rating is 4 out of 5 or higher.

## 9. Risks
| Risk | Fix |
|---|---|
| Nobody wants to teach | Start with popular skills and invite student clubs |
| Unfair swaps (one person gives more) | Show clear swap terms before accepting |
| Safety when meeting | Meet in public campus places, and use report and block |

## 10. Timeline
- **Week 1-2:** research and design
- **Week 3-6:** build profile, matching, and chat
- **Week 7:** test with 20 students
- **Week 8:** launch