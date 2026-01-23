# Report
In this repository, I am presenting both my files and a report where I comment on what worked out and what did not.

(Disclaimer: **I did not use any kind of AI for the encoding**. During the last lecture, I tried a few prompts and the results were not good at all. So I decided to not include it into my workflow at all, solely relying on the Guidelines and the things we've learned during the course.)

### Motivation

When we were told to look up a suitable piece to encode, I wanted to find something that a) included new concepts I haven't used in MEI yet and b) is not longer than 20 measures. After doing a little bit of research, I decided to try the *VI.* from *Schoenbergs Sechs kleine Klavierstücke, Op.19*. At first glance, I already discovered several things that I knew would become difficult to encode, such as the additional third line during the last few measures, multiple layers within the staves (partially even within triplets), etc.
In my opinion it is a perfect piece to practice key concepts of MEI music encoding because of its high density of encoding questions covered in only a handful of measures.


### What worked well
In general, I am positively surprised how much can be done in MEI despite not being very experienced in terms of music encoding. 
Learning the basics such as how to place notes, arrange chords and adding accidentals was relatively intuitive. Due to the fact that the mei-friend automatically assigns @xml:id attributes to every encoded object, jumping to a specific measure or an exact note could also easily be done. Despite that, I quickly faced problems that were not solveable to me at first, such as changing the exact height of the `<pedal>` element in measures 5&6. At some point I was able to fix this issue because I figured out that the @ho and @vo attributes can be used in scenarios where the positions of certain elements in the score have to be changed in order to be matching with the reference-sheet. 

**Before (@vo / @ho not adjusted):**

<img width="263" height="140" alt="image" src="https://github.com/user-attachments/assets/e1bb2d69-2492-497c-be61-3e5afda4e972" />


**After (using @vo):**

<img width="274" height="146" alt="image" src="https://github.com/user-attachments/assets/d687223c-57e8-46ef-a804-7dbc0f883307" />

Another interesting aspect of MEI that I've discovered is the usage of either the @tie attribute or the `<slur>` element. From my point of view, I figured that @tie is very useful in situations like this:

<img width="429" height="137" alt="image" src="https://github.com/user-attachments/assets/8a9dbd81-29c2-4538-81ea-54a62e8fa5b6" />

Here, the same pitch is being held across multiple notes.
Whereas in other situations like this:

<img width="471" height="142" alt="image" src="https://github.com/user-attachments/assets/05113b07-315d-4a1c-ac46-49ce44487819" />

connecting the highest notes of the chords has to be done with a `<slur>` element. 
Also, in Chapter _4.3.2 Ties, Slurs and Phrase Marks_ of the Guidelines, there is explained that slur can also be encoded as an attribute. However, I did not really try that in my encoding because I was already kind of used to creating slurs as elements.

During the course, we already figured that using @tstamp and @tstamp2 instead of @startid and @endid in a <slur> element creates a different slur. In most of my cases, I went with the id-approach because oftentimes a more "tight" connection of the slur was needed. 

Placing accents with an `<artic>` element within the `<note>` element was very convenient and by adding a @place to it, defining the location also worked out fine.

Furthermore, encoding that accidentals stay the same despite not explicitly written (like the f sharp in measure 1) has to be done with the @accid.ges attribute within a `<note>` element. One thing that confused me was when I looked up Chapter *4.2.5.2.1 Chords in CMN* of the MEI Guidelines. In the according example, there is a C-sharp minor excerpt (*Figure 12*) and directly below it, there is an excerpt of the encoding (*Listing 133*). I do not understand, why adding @accid.ges is needed for notes that are already sharp by definition due to the key signature of C-sharp such as C or G...


In addition to that, adding metadata within the `<meiHead>` also worked out fine. However, the metadata-section was not my primary focus because I first wanted to learn how to properly encode the music itself before doing a deep-dive into aspects like adding metadata. 


### Problems

- What does not work and why? Compare comments in the mei-document
- What did I try to fix it?

- M. 8; We have two layers and `<rest>` element within `<tuplet>`; I could'nt figure out how to only show one rest that counts for both layers. Tried: `<space>` instead of rest, this shoves the triad.
- Rendering first 2 staves and then adding the 3rd staff; splitting the score into two separate `<mDiv>`s did not help either. Compare file *mDivSchoenberg.mei*

e.g. 
- fonts 
- determine exact positions
