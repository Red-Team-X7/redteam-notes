# Learning Process

Tags: #🧑‍🎓 
Related to:
See also:
Previous: [[HTB Academy]]

![[logo_learning_process.png]]

The learning process is one of the essential and most important components that is often overlooked. This module does not teach you techniques to learn but describes the process of learning adapted to the field of information security. You will learn to understand how and when we learn best and increase and improve your learning efficiency greatly.

### Module Summary

This module covers various stages of the learning process, such as:

-   Mindset
-   Learning Efficiency and learning types
-   Documentation
-   Organization
-   Focus
-   Attention
-   Dealing with Frustration

The principles covered in this module will benefit you greatly as you embark on, or continue, your infosec journey.

# Mindset

## Way of Thinking

---

The field of information security is massive. It would be impossible for any one person to learn everything. Let us take the following example:

>Imagine you want to become a programmer, and you know that there are more than 200 different programming languages that can be used to create applications that can be cracked by debugging or reverse engineering. If we learned every programming language within 100 hours, we would spend 20,000 hours or 2,500 days (8 hours per day) or, in other words, almost seven years to learn all of these programming languages. As a result, we spent seven years learning all these languages and never tried to debug or reverse engineer the program we created. Great! Let us spend another seven years learning to debug and reverse engineering.

We have got the idea. No one wants to spend so much time on just one area. Furthermore, this is not necessary. We will need some time to learn different technical principles, structures, and processes, but we will not need to spend seven years. Every programming language has its own strengths and weaknesses. Also, if we can obtain a deep understanding of a single programming language, we will learn others much faster. We do not need to learn every programming language to understand how to read their code. All of them follow the same principles which R. D. Tennent initially defined:

1.  The Principle of Abstraction
2.  The Principle of Correspondence
3.  The Principle of Data Type Completeness

In information security, we have to learn and understand these principles, structures, and processes quickly. Additionally, we have to adapt our knowledge to the various environments we encounter. We will have many situations where we will not understand how "it" works. That is good. At this point, we have to find out what we do not know. More about that later.

There are many learning-focused information security communities available to us. Many of these communities provide free reviews of tested applications, vulnerable machines, and guides to help each other and improve their members' skills. When we speak with the other members, we will notice there are generally two types of people.

-   Those that do not know anything.
-   Those who think they do not know anything.

This can be very frustrating, and this is a normal part of the learning process. Communication within these communities should be respectful, always keeping in mind that we all started with zero knowledge of this field. This is a critical point of success for the community and everyone learning and working in this field. Within Hack The Box, we can use the Forum and Discord server to interact with the community.

-   Forum: [https://forum.hackthebox.eu](https://forum.hackthebox.eu/)
    
-   Discord: [https://discord.gg/hackthebox](https://discord.gg/hackthebox)
    

Another important point is our knowledge level. Many people do not know their actual skill and knowledge level. This is a complicated topic because penetration testers must have a deep understanding of a wide variety of technologies. As previously mentioned, the problem in this field is the sheer volume of information available to us. We can learn about every topic and still not master any one area, or we can learn about just one topic and become an expert in it.

Another option is developing our research methodology, the learning process, and how to use this to improve our knowledge. We will be successful if we know how to search for the required information on the internet, and we know how to learn fast and adapt it to the environment we are working in. However, before we can do this, we have to learn and practice how to do it.

We will become a good penetration tester only through considerable practice. There is no other way to improve our practical skills. For example, we can read 50 books about programming, and we will understand how to read the code. This is the process of passive learning. This can be useful. However, if we need to write our own program, we have to practice active learning, which means we have to write code and test it on our own.

One of the most common questions is:

>When is a penetration tester good enough?

We know that one person cannot know everything. In this case, we have to learn how to `find`, `choose`, and `adapt` the information we need.

Right now, we are considering these three key terms. There is one key term missing.

Which key term is missing from the above list?

The crucial missing term is: **`LEARN`**

The process of "learning how to `learn`" is not easy. Most people have never truly learned how to learn effectively. For example, in school, our teachers discussed some topics with our class. First, teachers show us just one way to solve a problem. They explained one way to solve the problem, and after that, they gave us exercises to practice further.

Let us take a closer look at the problem. Look at this simple math equation and try to solve it:

>20 * ________+ ________ = 65535

This equation is easy to solve, but did we think about how many different ways are there to solve it?

##### Optional Exercise:

>Ask yourself why you didn't solve the problem in a different way. Write it down and try to think about the reasons for choosing the method that you chose. Take as much time as you need for it before you continue.


## Think Outside the Box

* * * * *

What limitations were you given for this exercise? - None.

So, why didn't you think to add more digits or to replace the given arithmetic operations?

Welcome to the hacker's way of thinking called:

"`Outside the box`."

So, why didn't we think like that? During this learning path, we will acquire more information that will help us find an answer. However, first, we have to understand the way of thinking we currently use. Make it clearer. Try to understand what we have to work on.

##### Optional Exercise:

>Why didn't you consider changing the arithmetic operations? Why didn't you think to add more digits? Try to answer as detailed as possible on your own. Try to write about it in at least 200 words.

## Occam's Razor

* * * * *

Thinking outside the box helps us cross imaginary boundaries and thus to access possibilities and options that were not recognizable to us at first. Thereby, we will encounter many options, and the whole way to the solution of a problem can become very complicated very fast. The Occam's Razor principle is beneficial for simplifying these circumstances.

Occam's Razor is one of the central principles of modern scientific theory. The principle is based on the following definition:

-   `The most straightforward theory is preferable to all others of several sufficient possible explanations for the same state of facts. In other words: The simplest explanation is always the most probable.`

For example, we can assume that our computer has stopped working. There could be many reasons for this, as we can already imagine. It can be because the power supply is faulty, CPU issues, or maybe even the motherboard is fried.

With such or similar problems, we automatically start to list the possibilities of what could be the reason before we start to solve the problem. Many people work by the process of elimination. They eliminate the probable possibilities that could be responsible for the problem. This approach already leads us in the wrong direction and results in considerable effort to solve the problem. With this type of approach, most people would start by taking their computers apart and checking all of the connections. They are looking for the most likely cause but ignoring the simplicity factor.

After all, the question we should be asking is:

-   Why is our computer not getting power?

When we ask this question, we automatically form associations in our minds that have to do with the word "power ."In this approach, the first thought is usually focused on the power supply. The power supply regulates the power for a computer. Therefore, most people's first thought is that the power supply has a defect and is no longer functional.

Nevertheless, let us not forget to think outside the box when we think of "power ."Because if we set ourselves the limits that it can only be our computer, we limit our options considerably. If we leave these limits, the first point of contact from the computer is the connected socket and the multiple plugs. If we followed this approach, we would see that our multi-plug had been switched off; therefore, the computer had no power to start up.

So, in this case, the most straightforward explanation was also the most probable.

* * * * *

### Occam's Razor in Practice
-------------------------

Using Occam's Razor in practice sounds easier than it is in practice. We can state that the simplest explanation is the most probable. However, the fact is that apart from that, it is not always so. We must also distinguish between the individual details and mechanisms and the general picture or concept. In our learning phase (and thus also during our penetration tests against companies), we will encounter many situations in which we learn something new. However, it is crucial to understand the overall concept rather than the individual steps involved. For example, once we are familiar with SQL injection and how it occurs, we may find the individual steps difficult at first. However, once we understand the overall concept, it will be easy for us to discover when a web application is vulnerable to SQL injections.

If we have already dealt with SQL injections and know how they can look, we also understand that the individual steps to detect and exploit them can be very complicated. Nevertheless, what remains the same is the concept. The concept is the main focus when learning new topics.

Another example is the approach to penetration testing, which is very common throughout the cybersecurity community. Everyone discusses the cases that can occur and how best to approach them. Let us think back to Occam's Razor principle and think outside the box.

Anyone who has done at least two or three penetration tests will find that each one is unique. Even if the same systems are used for the clients and servers, their configuration is typically unique. The unique aspects are the stages in a penetration test, which we can learn more about in the [Penetration Testing Process](https://academy.hackthebox.com/module/details/90) module.

`The simplest explanation for the best approach to penetration testing is that we work with the information we can get.`

The unique techniques of how we get and use this information are, again, individual steps followed and not the whole concept. The same applies to most exploitation attacks and the individual steps for them. Once we understand the overall picture, adapting to the given situations and conditions is much easier. However, suppose we have only learned the individual steps. In that case, we will have difficulty adapting them to new situations because we do not understand their impact on the systems and their applications.

Later in the process, we will see this phenomenon again and again. Once we have identified the solution to the problem, the process and the steps required to achieve it seem pretty straightforward in most cases. Looking back, it always seems easy once we know the solution. The art, after all, is not to get some flag but to find the way to it.

## Talent

* * * * *

We all know one or two talented people in our circles of acquaintances. These are people who, in our opinion, bring incredible performance in one or another area. Most people believe such talents and abilities are innate and that these people have strong skills in these areas due to their genetics or other intangible factors. Besides the fact that genetics influence our thinking processes, talent itself is not innate---the ability to solve particular problems with excellence results from thought processes developed primarily in early childhood. Children can develop such a talent much more effortlessly than adults. This is because they have not yet developed complicated thinking and do not have complex hurdles to overcome. In other words, children typically do not overcomplicate things like adults do.

There is no precise definition of talent. Because the official definition is that talent is a natural aptitude or skill. Natural in this sense means that it exists in or is caused by nature. Nevertheless, it cannot be valid if we consider it carefully because this would have to apply to any skill. Then let us ask the following:

-   Who among the several million students on Hack The Box can naturally fly an airplane?

Starting and taking off an airplane requires considerable technical knowledge, which differs based on the type of airplane. Maybe there will be one who, with luck and without knowledge, manages to start the plane and drive with it a few meters, but taking off requires knowledge of the controls and physics. No one knows how to fly an airplane naturally without considerable training and practice.

This definition leads us to believe that masters of their craft are born. This is a misconception that comes from the interpretive ability of humans that we must abstract from. However, in summary, talented individuals are defined as highly efficient and perform exceptionally well in their individual fields.

Such talents, or rather the ability to solve specific problems and challenges with high efficiency, arise from the `constant or persistent` confrontation with the corresponding situations and the problems that arise. However, it does not have to be precisely the one situation to develop talent but rather the thinking pattern to solve problems. The confrontation expands the so-called comfort zone and repertoire, which allows us to think more easily and tackle the challenge or problem. In essence, talent is a trained and adapted thought process and the associated thought patterns for specific fields and situations.

However, we know that we have a good influence on our thought processes and thought patterns and can influence them according to our decisions. This means we can develop and train such talent for any field we want.

We should keep in mind that we are not born with our talents/skills. A newborn baby will not suddenly start speaking in 5 different languages or explain to the doctor which laws were not adequately followed during childbirth. However, if we have a guitarist who has been playing guitar for years, it will be much easier for that person to learn to play bass guitar than someone who has never played a string instrument. Nevertheless, let us take a slightly more complicated example where the differences become much clearer. Even a drummer will find it easier to learn to play bass guitar than someone who has never played a musical instrument.

Drummers have a great sense of rhythm and emphasize certain parts in each measure. Good drummers keep the rhythm for the songs played and highlight and support the other instruments and vocals with different combinations and variations. Thus, a drummer has already learned many skills needed to learn bass guitar. The drummer will then focus on completely different skills that an inexperienced student has yet to develop in learning to play bass guitar. If we put the drummer and the inexperienced student in the same room, the drummer will be perceived as talented.

Developing talent in childhood often depends mainly on the parents and how they encourage their children. If a child enjoys something, or at least it is presented as fun by the parents, and the child engages with it, it learns to deal with the given situation. This opens up new possibilities for the child, and new thought patterns are formed, which will be followed by the thought processes first. To understand how these thought processes develop, we would have to deal in detail with psychology and neurology, which goes far beyond this module's scope. However, the important thing is that we influence the development of our thought patterns, thought processes, and thus also our talents.

We consider someone talented when they learn something new quickly or grasp its functionality. Calling someone talented is, basically, a status assignment. We consider all our students talented even if we do not know their "talents." However, we understand that any kind of individuality in our students' thinking patterns will help them solve different situations in a way that will bring out their talent. In most cases, our students will inevitably discover for themselves what their talents are over time and practice. The problem is that the variety of situations that arise is so extensive that it is difficult to identify these talents in penetration testing.

# Learning Dependencies

## Way Of Learning

* * * * *

So, let us jump back to the math exercise from the first section.

>20 * ________+ ________ = 65535

Why did we calculate the math task like this?

We performed the calculation the way we learned it. That means we will use the patterns we have been conditioned to use. At this stage, as in the previous example with the calculation, we used the information we already had. This art of thinking, called "`Outside the box`," is an essential part of the "hacker mindset", or the way we must think as penetration testers to solve complex problems. Thinking outside the box means seeing things outside of the limitations placed on us. This means we have to be able to "pivot." We have to focus on so many different technologies during our penetration tests that it can become confusing and frustrating when we do not understand some things.

`A problem is an emotional state. Without emotions, it is just a situation.`

In other words, frustration and confusion come with the point of view we are looking at. The learning process is not just a theoretical and practical part. It is also our learning process and progress that largely depends on our `emotional state`. If we feel good and we know we will reach our goal, we will be successful.

Another essential part that makes you successful is that you `know your goal`. Imagine the following scenario:

>You're standing still in a room, and your instructor instructs you to move across the room, and you start moving. After a while, the instructor put a chair in your way. What will you do? - You may sit down on this chair.

Now let us change the scenario a little bit.

>Your instructor instructs you to move to the other corner. We start moving, and the instructor puts a chair in our way again. What will we do?\
You will pass the chair and continue moving forward to the corner because you know your goal.

The big difference between these two scenarios is that we `know our goal` and know how we have to move on. We will overcome the obstacles which are put in our way. If we do not have a goal, we will stop at the first obstacle. Without a goal, we will be disoriented moving from one topic to another.

##### Optional Exercise:

>Write down the goal you want to achieve with this course as precisely as possible. Try to break it down and describe it in 500 words at most.

## Learning Efficiency

* * * * *

The problem here is the sheer size of the information security field. As we saw in the example with programming languages, there is a lot to learn and many topics to cover. Many of the courses available are very technical. This is a good thing and essential for us to strengthen our skillsets. We have to understand how things work, how they are structured, and how to use them. All of the technical information we need to be successful in this field is already out there.

The primary and most difficult objective we must overcome is the `combination` of our knowledge, adaptation, and new information.

It often is not easy to find the information we need. First, we have to find out what kind of information we need.

-   `What do we already know?`
-   `What do we not know yet?`

Even if we find the information we need, we do not know how to use it because we do not have an overview.

Another major problem we must solve is handling this massive amount of information and adapting it to our strengths and weaknesses.

Imagine another scenario:

>A student wants to learn how to assemble an engine. Before a student "can" assemble an engine, they start learning many theoretical concepts to prevent failure.

However, first of all, we have to fail. It is an `unavoidable` and `essential` part of `learning`. This is one of the parts of the learning process which make us successful. Experience is built on failures. It explains that we know how to handle differently. Sometimes adverse, situations where something does not work as expected.

`Academy` is structured in a way where the student starts to assemble an engine guided by the instructor. We will learn what we need, how to use it, and how to work with it. We will see what kind of things can happen, collect our first practical experience, and improve our existing skills. When a student was taught by an instructor who supported them and showed them how to assemble an engine, they would know how to do it independently. Moreover, the student can now learn all of the theoretical aspects more in-depth through practice and repetition.

In Academy, we will learn not only the basics of penetration testing but also how to:

-   Learn faster
-   Structure our knowledge
-   Find the information we need
-   Get the overview

Many companies are searching for good penetration testers and information security specialists.

>"However, what does it mean to be good?"

To be good at something means we know `what we are doing`. If we know what we are doing, that means that we are `experienced` with this topic. Experience means we have a vast `repertoire` in this field. Repertoire comes from `associations` and `practical experience`. When we say practical experience, we want to know how much we have to practice to become competent at a specific task.

There is something called the "10,000-Hour Rule," which explains that you need to spend 10,000 hours on becoming good at something. We do not want to spend 10,000 hours learning a skill.

When we research this rule a bit, we will find a TEDx talk by [Josh Kaufman](https://ideas.ted.com/dont-have-10000-hours-to-learn-something-new-thats-fine-all-you-need-is-20-hours/) in which he explains it more in-depth. He proposes that we can learn something new in 20 hours, even working on it for just 45 minutes per day. This sounds much more attainable! At this point, we also should think about the [Pareto Principle](https://en.wikipedia.org/wiki/Pareto_principle), or the `80/20 rule`.

The `Pareto principle` states that with 20% of the effort, we can achieve 80% of the effect. Conversely, this means that with 80% of the effort, we can achieve the remaining 20% of the effect, which is 100% missing. However, it is essential to note that it does not apply to everything but is a general rule applied to specific areas.

The whole section above is an example of a simple association where we combine different approaches and information.

As Josh Kaufman explained, we can become excellent pretty fast. This is the so-called `learning curve`, including active and passive learning. These active and passive learning types can be found in the [Learning Pyramid.](https://en.wikipedia.org/wiki/Learning_pyramid)

##### Optional Exercise:

>Collect as much information as possible about the "Learning Pyramid" and create an overview of it. Analyze your research process and document it. We will need it later.

## Learning Types

* * * * *

The Learning Pyramid can be represented in many different ways. It describes the learning efficiency of different types of practice.

* * * * *

### Passive Learning
----------------

If we follow the Learning Pyramid while going through the modules just by reading, we will learn only about `10%` of the whole penetration testing experience. By watching some demonstrations, we will not learn more than `30%`.

* * * * *

### Active Learning
---------------

When we start to discuss our entire enumeration process, results, and findings with others, we will see different points of view, results, and information to compare with our own and find out what we missed. By using this type of active learning, we collect up to `50%` experience. Before we can discuss our results with others, we should practice on our own. So while we practice, our learning experience grows to `75%`.

We can imagine when we learn theory in driving school. We learn a lot about car and traffic rules. Using examples, we are shown situations that should lead us to specific actions and reactions to ensure road safety. We can learn as much as we want, but as soon as we get into the car for the first time, we will realize that all of this knowledge has still not taught us *how* to drive a car.

Before moving on to the next exercise, we should talk about the information we collect. The information has a certain level of `quality`, but not all information is helpful. More than that, some information can confuse and disorient us completely. To learn to discern such information, we need a `repertoire` which we collect `by practicing`. Therefore, it is essential to understand the context of the topic we are researching.

Efficiency depends not only on the quality of information we find but on the usage of that information.

Moreover, it depends on our `motivation`, `focus`, and `our goal`.

There are many different ways to stay motivated. An excellent method that works very well is by recognizing success, even the most minor successes. We must recognize our successes and see that we have made progress. We already talked about how important it is to have a goal. When we know our goal, we know the direction of our actions. If we are focused on our goal, we will notice when we drift from our path. By following our path, we will automatically look back and see how far we have come. At this point, it is vital to notice the `progress` we have made.

`Progress is noticeable when the question that tortured us has lost its meaning.`

Looking back and seeing how far we have come will keep us motivated. Many people struggle during the learning process because they have to learn a lot of different topics. It is vital to take breaks and remain calm.

For example, if we attempt to force ourselves to learn Web Application Penetration Testing in two hours, it just will not work. There is too much information to handle and too many details inside the technical processes we must master.

To make it more clear, we will look at another example:

>How do we empty a bottle of water? We turn the bottle around and let it flow, right?\
Why didn't we try to create a vortex by turning the bottle around the Y-Axis?\
By creating a vortex, we let oxygen flow into the bottle regularly, and the water can flow out without closing the bottle opening.

The same thing happens with learning. If we learn too much without taking breaks, we will get stuck.

>"So, how many breaks do we need and how long should they be?"

This is a question that we must answer on our own because only we know what effects and consequences our actions will have on us.

However, what happens when we get stuck? There are many ways that we become "stuck". It could be that we focused too much and lost the context of the task at hand, or we are tired and did not take enough breaks. Solving a problem like this requires `creativity`. In penetration testing, it is essential to pay attention to details that appear unimportant at first glance. If we look back, we will see some terms printed in bold and `green`, and if we take a closer look, we will see that they have an essential meaning in the process. Here it is crucial to train the eye to notice even the most minor details. All our knowledge and experiences are based on associations that connect us with different perceptions, such as colors and smells, for example, through different situations, known to us as memories. These will be recalled later either actively or passively.

This process also only takes place in the course of practice. In the next step, we will see how important it is through a small practical example.

##### Optional Exercise:

>Collect as much information as possible about creativity and problem-solving. Put all the information together and create an overview. Find the best way for us to think creatively.

## The Brain

* * * * *

We need to familiarize ourselves with our brain and get to know some of its components to understand the role of the upcoming sections better, how they are structured, and how they can influence our learning process.

Our brain is a fascinating organ that makes us who we are. It is also the most unexplored area we know. There are also many myths that we all know. One is that we use only 5-10% of our brainpower. It is a myth that is entirely false. Our brain is always active in all regions. This has been tested in many different studies using electroencephalography (EEG) and functional MRI (fMRI).

Another frighteningly strong myth that has become entrenched in all kinds of societies is the belief that how fast we learn something says how intelligent we are. However, most people do not even know that the brain regions responsible for the most difficult logical tasks do not develop until we're 20 (+/- 2) years old. Only then is our brain developed to the point where we can solve such tasks. This is because each person needs a different amount of time to develop certain brain regions.

One of the best-known examples is Einstein, who we know was terrible at math and learned very slowly throughout his school career, unlike the others. We also know some people who were very bad at school in one subject but are unbeatable in another. Without going too deep into cognitive science, neurology, psycholinguistics, and psychology, this is an indicator of the development of specific brain regions of the human body.

Another good example where this can be seen and is widely used is the image of a computer nerd who is very good with computers and seems to know them inside out but has severe social deficits. This, too, can be traced back to the development of specific brain regions because the brain changes on a physiological level when we learn something new.

Even though we seem quite unaware of the organ and hardly understand how it works, over the years, we have discovered methods that have specific effects on our brain in many ways, which we will discuss throughout the rest of this module.

Until now, cognitive science has not been able to prove what a thought is. However, cognitive science is an interdisciplinary science that studies conscious and potentially conscious processes in which conscious and subconscious minds are explored. We have many different cognitive abilities, such as memory, language, perception, problem-solving, mental will, and many more. We will discuss some of these to the point of recognizing their importance and impact. The only thing scientists have agreed on so far is that thought is not material (at least, it has not been proven yet).

* * * * *

### The Theory of Thought
---------------------

The following definition is my personal view and how I see thought. Most scientists coming from brain research will probably disagree with the following definition of thought here because of many personal or professional reasons. But since they do not have an answer either, I will share my definition of thought here that I have not been able to disprove (yet).

-   `A thought is an individual process (action/reaction) to one or more influences (internal/external) in which information is interpreted and linked inwardly according to our personal methodology (developed through our existing lifetimes).`

To better understand this definition, let us consider the following example:

-   Scotland has 421 words for "snow."

When reading such new information, an individual process is started, in this case, for most, a surprise (`reaction`) to an influence (`external information influence`) that we inwardly imagine (`interpret`) and process (`link to known knowledge`).

Working on this theory further, we find that at some point, we will have a series of nodes linked to different information (Scotland - Snow - 421 - Words). Such links are also called associations. We know that our memory and information processing in different situations work based on these association chains stored in our neuronal networks.

Scientists have discovered that our brain is constantly working and that we are continually producing thoughts. However, the latest research has led cognitive scientists to an inconclusive result. They cannot say precisely whether the brain works more actively during our waking or sleeping phases. This is because each of us has a subconscious and a conscious in which the thoughts are processed. This has been proven by the [Libet Experiment](https://en.wikipedia.org/wiki/Neuroscience_of_free_will) and that conscious decision, respectively, the conscious experience is delayed after the neuronal processes.

* * * * *

### Conscious Thoughts
------------------

Our consciousness is also a very complex topic with many views and definitions. Also, this has not yet been researched enough to say how it works in detail. We do not need to know every detail for our purposes in this field to benefit from it. However, we should understand what we are talking about when we talk about conscious and subconscious. For us, however, the following definition is sufficient for the description of human consciousness:

`Consciousness describes the totality of all those mental processes by which we become aware of the external and our internal world with active observation. Therefore, when we actively observe that we are looking at a monitor full of text and can decide to change the situation if necessary and intentionally look elsewhere, we are in consciousness.`

* * * * *

### Unconscious Thoughts
--------------------

Psychology knows another level of consciousness, the so-called subconscious. Thoughts that arise in our subconscious, we do not perceive superficially. What we do perceive are emotions. Emotions reflect the way we think subconsciously. We process far more thoughts subconsciously than consciously.

Nevertheless, subconscious thoughts influence what we do. Studies have shown, among other things, that the subconscious mind has already made a decision 30 seconds before we become aware of it. One of the first people to study the subconscious mind was Sigmund Freud, who lived about 100 years ago.

Part of Libet's experiments showed that the difference between conscious and unconscious experiences could depend on the duration of brain activity. In these experiments, subjects were given stimuli to the ascending sensory pathway in the thalamus. For example, the subjects saw two lamps, each of which was illuminated alternately for one second. Subjects were asked to say which of the two lamps was lit when the stimulus was administered. If the stimulus lasted for less than half a second, they did not consciously perceive the stimulus. However, even if they did not consciously perceive a stimulus, the subjects were asked to guess which lamp was lit while the stimulus was administered. This showed that even if the subjects were not consciously aware of the stimulus, they guessed correctly much more frequently than at random (50 percent). When the stimulus lasted 150 to 260 milliseconds, the subjects guessed correctly 75 percent of the time. For the test subjects to perceive the stimulus consciously, the stimulus had to last 500 milliseconds.

## The Will

* * * * *

The term will is a concept interpreted differently in many disciplines. In psychology, will is considered a descriptive construct that presupposes a conscious decision to act, and thus, it is primarily associated with rational action.

Will is used in different contexts and has several meanings: the mental act from which an impulse to achieve specific goals emanates and the setting of goals, and the ultimate translation of these personally or collectively made decisions into action, that is, into conscious and deliberate or even planned action.

From a philosophical point of view, will is defined as deciding on a particular type of action based on the motives for acting consciously. So let us say will is the effort to perform a certain action or achieve a specific goal. Therefore, it is most relevant for us to have decided to achieve a goal that we have determined and strive for it.

Before we decide to achieve a specific goal, we must become clear about our desires. In as much detail as possible, we should explain to ourselves what we want and how it must feel to achieve our goal. This process can also be thought of as dreaming, where we imagine a situation we would like to be in. Unfortunately, most people stop dreaming shortly after they start because they do not see a way to get there.

These people overlook the essential component that the path plays absolutely no role in how we reach that goal because, ultimately, our path is only created by the steps we take.

We can look at interviews of the most famous actors, developers, and scientists, and we will see that none of them have planned and foreseen their careers in the way they came about.

Desire is very dependent on the belief in it. When we believe in our abilities, it relieves us of our complexes (at least from some of them), and we get access to chains of associations of our thinking, interrupted by the pressure of our fears. Let us remember and deeply internalize the following sentence:

-   `Fear is a state and the product of our imagination of the future and its consequences where the present is suppressed.`

Fear is essential and healthy in life-threatening and health-threatening situations. However, sitting in a chair in front of a computer, afraid of not being up to the tasks we find here, is irrational. After all, we have not yet worked through most of the material, but we are already beginning to program (adjust) ourselves to fail. So let's ask if this fear is real:

-   Have we already worked through all the material?
-   Have we already seen what is being taught and how it is being taught?
-   Do we already have to have the skills that are expected of us?

If we answer "no" to these three questions, it should be clear that we are afraid of something without even trying it. This leads to the fact that the fear, in this case, is not real.

It is interesting that, especially in our field of penetration testing, many students react paradoxically. Most of those who feel a particular "fear" during learning are unaware of what they are afraid of. They believe they are afraid of failing and not learning something well enough, but sometimes as soon as they get stuck on a subject that is not easy for them, they give up. Nevertheless, is not that the failure they were afraid of all along and wanted to avoid by all means? Actually, yes. However, these types of students find it easier to give up and fail than to keep learning and improving. Getting better inevitably happens when we keep practicing and trying different approaches.

We must keep a clear goal in mind to prevent this from happening so quickly.

## The Goal

* * * * *

The term goal refers to a state that lies in the future, generally changed from the present, desirable, that we aspire to fulfill. A goal is thus a defined and desired endpoint of a process. Therefore, it must be possible to determine precisely from the formulation of the goal what the desired state must be for a goal to be considered achieved. There are many different types of goals, such as:

|  |  |
| --- | --- |
| Quantitative goals | Qualitative goals |
| Complementary goals | Competing goals |
| Indifferent goals | Main goals |
| Secondary goals | and many more |

For every single goal, dozens of different formulas and models have been created to achieve them in the "best possible" way. However, finding a suitable model that fits our personal needs, life experiences, and goals is not easy. Each of the models has a different focus, and to find the perfect model for us, we would have to study each and try them out for a more extended time. The biggest problem is that we are forced to abandon one of the models because we do not know if the model will lead us to our goal, and in addition, efficiency conflicts with comfort. If we feel comfortable with this model, it does not mean that it is effective and will lead us to the goal; therefore, we would have to try another model to find out. Without knowing how the rest of the models affect our effectiveness, we would have to try all the others, which can be very time-consuming.

The results of a meta-analysis of over 200 studies with more than 40,000 participants show that over 90 percent of people are significantly more successful in achieving their dreams by `setting challenging and specific goals`.

We cannot emphasize strongly enough the importance of setting a clear goal for ourselves.

What do we want to achieve? Do we want to...:

-   Pass an exam?
-   Obtain a certification?
-   Learn and master new skills?
-   Or impress and please others?

As we can certainly already think and imagine, we will take different "paths" depending on the goal we have set for ourselves. There is even a big difference between passing an exam or just getting the certification for it. Many think that the certification proves that the trained skills have been acquired. However, for most, the certification is a formal and official acknowledgment of participation in particular training. For example, if we only want to get the certification or even just the confirmation of having completed something, we will look for the easiest way to get closer to that goal as quickly as possible. Decisions are made to ask someone how certain tasks are solved in order not to have to think about it.

An essential part of this is that by avoiding our own "thinking" (or trying to solve the task on our own), we deprive ourselves of the possibility of creating chains of associations in our brain. These association chains are the links in our brain cells that serve our thinking processes and information links by which we learn to solve problems or situations. Thus, in simple terms, we deprive ourselves of the ability to learn something new and to develop further.

Because the decision of what goal we want to achieve influences how we learn, a task or goal helps us influence how we think.

Another essential aspect that we can look at, which is an excellent example, is how to reach this goal. If we think about it in more detail, none of the current "great" and well-known personalities will be able to say that they knew the path that led them to the goal beforehand. None of these people knew it. What they did know, however, was the goal that they had set for themselves.

Someone who claims that his way is the only right way should stick to that way if it works for themselves. However, claiming that there are no other ways may be true for that person, but it does not mean that others cannot do it. For example, metaphorically speaking, if the person does not know how to use a ladder, they will only get to higher floors with outside help.

No matter what goal we have in mind, we must decide on it.

## Decision Making

* * * * *

The decision-making process in which we make our decisions about certain situations is a very extensive and complicated subject on which there are many studies and disagreements. Many different theories and phases have been created to facilitate a better overview of the thought processes of the human brain. However, as we can already imagine, it is far from easy to define such phases as each has individual thought processes and patterns.

A decision is, in simple terms, the choice of one of several options. All decisions are made based on the importance of the circumstances. We make decisions based on what we expect to get the most out of it. Thus, decisions are made not only rationally but also emotionally. Let's look at a very rough and simplified situation to make it more straightforward.

Let's assume that we have spontaneously been given a day off by our employer and a friend has asked us for help. We are faced with choosing whether we want to use our available time for our project, which we want to present to our employer and expect a salary increase, or whether we want to help our friend move. If our well-being is more important to us than our own income, we decide to help with the move. On the other hand, if our income seems more important to us, we will choose to spend time on our project.

Research in decision psychology has established that people by no means behave exclusively in terms of cost-benefit considerations. Since many models of rationality do not realistically reflect actual decision-making behavior, a person's decision-making behavior can be understood as a process in which rationality occurs only to a limited extent.

Let us look at a well-known example, the so-called [Trolley Problem](https://en.wikipedia.org/wiki/Trolley_problem).

* * * * *

### The Trolley Problem
-------------------

The Trolley Problem is a thought experiment in which three different scenarios have occupied many philosophers, psychologists, and legal scholars for decades, and one of them is described as follows:

"A train speeds unbraked toward a group of five-track workers. The switchman might divert the train to a siding where only one person is working. Should he sacrifice one person to save five others?"

Try to decide for yourself while trying to figure out how that decision came about.

![[1920px-Trolley_Problem.png]]

70,000 people in 42 countries were surveyed, and the survey results were published in an article in [Proceedings of the National Academy of Sciences](https://www.pnas.org/content/117/5/2332).

The Social and Personality Psychology Compass researchers criticized that scenario because it is too extreme. If we stay in this situation, the decision will be pretty tricky. The researchers finally said that the example is too extreme because people cannot be expected to make such decisions, and it is basically "impossible" to make a correct decision. This statement has many different reasons.

1.  it is an enormous psychological burden before, during, and after the decision for the respective person.
2.  the persons representing this statement do not see a solution for this situation.
3.  and many other reasons based on personal experience.

This situation in which we have to decide is much more similar to the mathematics problem from the [Way of Thinking](https://academy.hackthebox.com/module/9/section/45) section than it appears at first glance.

-   `20 * ________ + ________ = 65535`

Because here we have at first sight only two options:

1.  either we switch tracks, and the train runs over one person
2.  or we do nothing, and five people are run over by the train.

In our math example, we must decide where to place the smallest number to make it as easy as possible.

1.  either we place it on the first open digit
2.  or we place it on the second.

In both cases, the procedure changes, but the result remains the same. So in the math exercise, the result is 65,535, and in the trolley problem, someone is run over.

Let's consider the following solution to the trolley problem:

![[TrolleyProblem.png]]

The red lines represent ropes, and the blue circles represent pillars that we have placed. The first thing that comes to mind is:

-   "But we are not allowed to place pillars" or.
-   "We are only allowed to press the switch."

However, the fact is that no one has told us whether we are allowed to move or not. We set our limitations ourselves, not by others. It is the same as if a stranger on the street were to tell us that we are suddenly not allowed to move while walking. Except for the fact that we will look at the person strangely, we will still walk (unlikely - but that is another topic).

If we learn to set these limits based on facts, our decisions will be much easier and, above all, much more effective.

If we take a closer look at the trolley problem, the first questions arise:

-   How far away is the train?
-   How fast is the train going?
-   How much time do we have to try to save everyone?
-   How can we save everyone?
-   What tools do we have at our disposal?

If we take a closer look, we will see that these factors are not given at all. They are missing, just like in the math problem. However, just as in the mathematics problem, no one has said that we must not change the circumstances (arithmetic operators) for this. Because any additional factor can change the decision entirely. An additional example of this would be if all the people on the tracks are conscious, we could save them all by warning them to get off the tracks as quickly as possible.

If we go to the extreme and say that the train will arrive in 10 seconds, it does not mean we have to choose one of the options given to us. However, the absolute extreme solution would be to flip the switch while the train passes over it. This is called "double-tracking" and will likely derail the train, passing the people.

We need to know the factors and assess the consequences to make a decision. The more factors we know, the more precise the decision we will be able to make for our goal.

If someone tells us that something is impossible, this person cannot possibly know all the factors with which we are connected. Just because the person believes that they see no solution for a task or goal, it only means that the person does not see a solution or a way to achieve the goal. Many people accept this, but they transfer this attitude to themselves, which leads to the fact that the desired goal or even the attempt is already given up. As a result, people fail before they even try.

If we do not know what to do in one situation or another, the reason is usually that we have not gathered enough facts to make a good decision. However, once we have gathered enough data, we can better calculate what result we will achieve in the end, and based on the facts we have gathered, we open up possibilities and paths we can take.

Finally, this means that no one will ever be able to question your success if you:

Decide (`Decision Making`) on the goal defined in detail (`The Goal`) that you really want to achieve from your heart (`Willingness`), and that will make you happy consciously and subconsciously (`The Brain`).

# Learning Overview

## Documentation

---

When it comes to documentation, we must first determine the report audience. We will document our activities differently than we would present our results to a customer. The purpose of documentation is to present the information we have obtained in a comprehensible and easy way to reproduce a specific activity.

Therefore the essential characteristics of documentation are:

1.  Overview
2.  Structure
3.  Clarity

As we learn and practice, we will come across many different situations and resources. As discussed before, we will have to process massive amounts of information.

There are many resources available for documentation. We recommend a tool called `CherryTree`.

It is essential to get clarity, and a picture is worth a thousand words. For this, we can use a tool called `FlameShot` that makes it easier for us to take screenshots and edit them directly.

No matter whom the documentation is intended for, here are some guidelines we can follow:

1.  It is beneficial to put ourselves in the position of our readers. This will make it much easier for us to design the documentation.
2.  Avoid repetition and ambiguity.
3.  Make documentation as easy to read as possible. No one wants to read the documentation that is difficult to understand or follow.

Before we create documentation for our customers, we can clarify which points are most important to them.

##### Optional Exercise:

>Do some research and find examples of penetration test reports and pick out the essential features. Get an overview of the following:  
 > 
>1) What topics have been covered?  
>2) How are they structured?  
>3) How are they presented?

## Organization

* * * * *

We have already seen the term `overview` mentioned several times. To understand how important this term is, imagine the following situation:

>You are standing on a big mountain, and at the bottom of the mountain, there is a vast forest. On the horizon, we see another mountain we want to reach. The difficulty here is that we will not see this mountain as soon as we go down into the forest. The only way to reach the mountain is to orient ourselves using the lakes, rivers, and fields between these two mountains.

This means that we should take all the necessary tools with us, like a lighter, knife, tent, and others, and set all the interim orientation points to avoid getting lost. Because as soon as we get lost, we cannot move through the forest disoriented, hoping to reach our goal somehow, or we will have to move back to the first mountain to reorient ourselves.

We can see how the terms depend on each other and how important it is to have a map to orient ourselves. By completing the previous exercises, we have already made the first drawings on our map. These will help us to understand where we are and where we want to go. Being organized is significant in penetration testing because the entire report writing process has to be structured.

It may take us a single day to take over several systems. So we don't want to keep looking for sources or information we need over and over again. Organization is best described in the following example:

>An inexperienced woodcutter takes 30 minutes to sharpen his axe and 3 hours to cut down the tree.
>
>The experienced one will sharpen the axe for 3 hours and cut down the tree within 30 minutes.

There are many different management techniques and methods that we can use.

These include:

-   Scrum

-   Agile

-   ToDo-Lists

-   Bullet Journal and more.

##### Optional Exercise:

>Create a list of different management techniques and methods that you can find and list all their negatives and positives. Experiment with the ones that suit you best and choose/create a method for yourself.

# The Process

## Focus

* * * * *

Let us dive a little deeper. This time we will talk about `focus`, which is a vital skill that we need. However, like many other abilities, it is a double-edged sword. When we talk about focus, we are talking about focusing on a subject for a specific time. When we focus on a subject, we concentrate most of our thinking and attention on the chosen topic. In doing so, all other thoughts concerning other topics will be completely faded out.

Have we ever wondered why most frustrated people go straight to the gym after a stressful day instead of just lying down and doing nothing? Why do they feel better afterward? Often we hear from them that they absolutely need it to calm down again. If you think about it a bit, it seems illogical at first because these people need additional physical energy in an exhausted state.

This raises again the question: "`Why further physical effort helps them to calm down?`"

On the one hand, so-called endorphins (happiness hormones) are produced by the body when doing workouts. These have different effects on the body, and one of them is the reduction of pain. Also, the chemical transmitters have a calming effect and ensure a restful sleep. Another function is the formation and regulation of hunger. We probably know the latter from sports. As soon as we have exhausted ourselves, the feeling of hunger comes. Another beneficial effect of endorphins is the strengthening of the immune system, not only on the physical but also on the psychological level.

This may explain why we start to feel better afterward, but after all, the most significant stress is not in the body but the mind. We know that after sports, the body is exhausted, but why does our mind start to relax? We are entirely focused on the physical exercises during the workout since these usually require a large amount of energy that also requires our entire focus. As the focus turns away from the actual stress, we let go of the situations that have stressed us so much, and these are `subconsciously` processed and, for the most part, solved. Here is an excellent example of such a situation that you have probably experienced by yourself:

>You have probably forgotten where you put something, or you can't think of a specific term that is so obvious to you. Have you ever asked yourself why you can suddenly remember it after a short time?

We distracted ourselves and focused on a different topic. With that, we gave our subconscious the possibility to solve the problem by itself.

It is essential to differentiate between `focus` and `attention` because they are not the same. `Attention` refers to the momentum, as it is happening right now, and you are reading this text. However, the `focus` is on the topic you are dealing with at the moment. When we return to the example of the misplaced keys, try to remember what was going through your mind. Most likely, it was something like:

>"Where did I put the keys?" or "Where did I last see them?"

If these were the questions we were asking ourselves, we could see from the questions alone that it is the subject of the keys, and therefore our `focus was on finding` the keys.

If you have been in the situation where you said to yourself at the same time:

>"OK, the keys are not here..."

Then we had our complete `attention on searching` for the keys. However, what if we are in a hurry?

Then we look at our watch every 5 seconds, and our thoughts are already on where we expected to be soon. We will hardly be able to `concentrate` on the search for the keys because your focus is on "being late" and not on "`finding the keys`." It should have become clearer that `focus` and `attention` are not the same and that attention is influenced by focus.

The focus is based on our will and what we want to achieve. It can be a `conscious decision` and a `subconscious decision` guided by external influences.

`Focusing is the purposeful and deliberate alignment to a specific goal`.

Focused people are not only enormously persistent and tenacious, but they are also hardly distracted or discouraged. If we know our goal, it is easier to align our focus accordingly. This, in turn, makes us much more efficient, and we get closer to our goal much faster and do not let ourselves be distracted by external influences.

## Attention

* * * * *

It can be said that attention is the perception of a specific topic with a higher level of interest in order to gather specific data and information from it.

Our attention changes with our experience and the information we gain from the content and its clarity.

`Attention is influenced by your interests, needs, personal attitudes, beliefs, orientations, goals, and experiences.`

We have already approached this module with a confident attitude, expectation, orientation, and goal. Attention is an independent `mental process` that takes place subconsciously.

So when we talk about concentration, we mean the maintenance of our attention on a specific topic. This means that as long as we are interested in a given topic, we keep working on it until we have achieved the desired result for our well-being. Again, attention goes hand in hand with concentration and focus.

We will already know that our attention will begin to decrease at some point, and we will no longer be able to absorb information effectively. We are getting stuck at this point, forcing ourselves to keep trying, and learning ends up with `problems` of understanding and, therefore, with higher `frustration`.

Information security is a vast subject, as we have already discussed. We will not be able to absorb all the information at once. We will often come back to topics and repeat what we are missing. This is a normal process. We must understand how to divide our attention.

There is no general formula that we can use to learn how to divide our attention correctly. This is an individual process that cannot be categorized yet without diving too deep into psychology studies. There are far too many personal characteristics and experiences of each individual to be taken into account.

We know that attention takes place at the moment and therefore has a limited duration to maintain it. It will be a great advantage to find out how long and emotional state our attention span lasts the longest.

* * * * *

We can document it, and after one week, we will be able to see an interesting pattern. If we want to approach this on a more scientific level, we can add the following points to our documentation to get a better insight into it:

-   current emotional state (calm, nervous, worried, happy, depressed, relaxed, etc.)
-   the previous flow of the day so far (also with one word)
-   place of work
-   working hours
-   duration
-   sleep
-   inserted breaks
-   duration of the breaks
-   and anything else we can think of.

These are phases for which we must invest at least one hour of our attention. Make it fun, and we will surprise ourselves with the discoveries that we make. We can create a simple list or even a table for us to document this quickly and easily. We do not have to document it every time we start something, but we could relate it to the current module/course/path.

* * * * *

Once we know how our attention span is behaving, we will also get an idea of how we can split it up. However, this does not mean that if we have an attention span of 60 minutes, we can divide it between 3 other topics of 20 minutes each. Remember that the amount of attention we can devote to a particular topic depends on too many factors.

Experiment with this. Change our place of work, working hours, duration of work if possible. Listen to different music and try out different things that might help us.

It would be best if we did not force ourselves to focus on a specific topic because it will have a negative effect and, as mentioned before, can end up in frustration, which we will discuss in another section.

`Make sure that you feel comfortable and ready to learn new things.`

## Comfort

* * * * *

`Comfort` is an `emotional state` of a person's mind, which, among other aspects, has a strong influence on behavior, thinking, focus, attention, and the ability to concentrate. This is the feeling of well-being in the form of comfort and the attitude of risk-free behavior. This is also often referred to as the so-called `comfort zone` in which the person `thinks`(`!`) he/she is located.

There is a so-called `Yerkes-Dodson` law, which describes the cognitive performance as a function of the level of stress/nervousness. The performance curve for this is also very individual, as it depends strongly on emotional and motivational factors and is divided into four sections.

The most used presentation of this law and the performance process is the Hebbian version.

![[NEW_yerkes-dodson-law.png]]

When it comes to comfort, it depends heavily on whether we have a healthy level of stress or have already crossed the threshold, leading to a reduction in our performance. It is very individual here where our center is. We are in an area that we are used to and that we consider comfortable. Mostly these are situations and fields in which we have already gained a certain amount of experience and know-how to find our way there.

When we leave the so-called `comfort zone`, we enter a situation or field where we have little or no experience. This kind of uncertainty lowers our ability to think and has a powerful impact on our thought processes, which, in turn, slows us down.

The fact that small children do not exhibit such uncertainty is interesting.

`They love to try out something new all the time and are not afraid or uncertain of making mistakes.`

After all, `mistakes are an essential part of the learning process`, and we should always keep it in mind.

An interesting question that arises here is: "Why small children, unlike adults, do not feel such uncertainty?"

Let us first look at the following diagram:

![[NEW_The-Comfort-Zone-diagram.png]]

>Now imagine you are standing at the entrance in front of a massive dark forest in the middle of the night. This forest is so dense that no daylight can get through the treetops. To the left and right of this forest, some cliffs are much too steep to climb down, and we know that somewhere in this forest, there is the one thing we want to have.\
Will you go inside and look for it?\
Common sense would do anything not to.
>
>But what if the thing you want is a hundred yards further into the forest, and it is brightly lit?\
That is the thing that will fulfill you the way we have always wanted it to.\
Would you risk it now?

Those who chose to leave the comfort zone would reach their destination faster than they thought they would. They would never have sprinted at such speed before in their lives.

Now we should understand the progression between decisions to step out of our comfort zone or stay in it. We will often get into situations where we do not know what to do. These will come again and again. However, we will always learn something new, and it will become more comfortable each time.

## Obstacles

* * * * *

Besides all the effective qualities we have come to know so far, many obstacles slow us down or even completely prevent us from reaching our goals, solving specific tasks, or acquiring and mastering skills. These are all factors that prevent us from leaving our comfort zone and daring to try something new.

* * * * *

### Fear
----

People are often afraid of something new, of something they do not know, and cannot evaluate if it could harm them somehow. There are many different types of fear. For us, however, only two are relevant for the time being. First, we need to distinguish between fear in dangerous situations and interpreted fear for the learning process. Fear in dangerous situations is necessary and serves to protect one's own life or those of loved ones. However, interpreted fear belongs to an imaginary state of fear. This means that we can feel fear without us being in a life-threatening situation, which the human body can even signal as pain because the fear is an emotional feeling (and therefore subconscious) that, in extreme cases, can even lead to the malfunction of the heart muscle ([Broken Heart Syndrome](https://en.wikipedia.org/wiki/Takotsubo_cardiomyopathy)).

An excellent example of such a fear behavior in human nature, which everyone knows, is the alien movies in which humanity fights against aliens. In most movies, aliens land on earth, and the "relationship problems" start. A more common example is when suddenly someone unknown bangs on our front door. At this moment we are surprised and get scared. After all, we do not know if it is a criminal or someone who needs help.

Imaginary fear is directed at events we imagine with consequences that we calculate. However, there is one crucial aspect that we cannot leave out:

-   `People fear what might happen in the future while not considering the present`.

Fear in non-life-threatening situations lies in the thoughts of the 'imaginary' future. In a future that we imagine and imagine ourselves. The more detailed we imagine it, the greater the fear becomes. Will Smith has also reported his experience with the confrontation with his fear.

<iframe width="560" height="315" src="https://www.youtube.com/embed/VsTBCQ2MnRM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Imaginary fear is an emotional state that keeps us from having the best experiences and prevents us from moving forward on the desired path. Even if we want to be excellent penetration testers, most beginners are afraid to put their maximum energy into it because of the imaginary fear of failure. This is due to many other factors that we will go into shortly.

However, if we find ourselves feeling such fear, then we should answer the following question in as much detail as possible:

-   "What of the reasons mentioned is real right now?"

Another factor that reinforces this imaginary fear and makes us think we will fail is our previous failures. One thing we should remember in advance, write it down and hang it on the wall where we can always see it:

-   `The difference between a winner and a loser is that the winner has lost more often than the loser`.

Failure is essential to learning and unavoidable. No one has ever acquired a skill without making a single mistake. It is quite the opposite. Our failures are crucial in our learning curve because they give us momentum to climb higher. In doing so, we reach a point where we have been before but already know what to expect at the higher level. This makes it easier for us to master this uphill climb because we have already slipped once at this point and know that we have to take a different path to get higher.

Many people give up here. We can think of it as just sitting there hoping we will get higher without moving. Even if a rope is handed to us from above, which we can use to pass the spot, it will not do any good if we do not move.

* * * * *

### Mindset
-------

It is in these situations that our excuses come up, like:

-   I cannot do this
-   This is not for me
-   I do not understand this
-   etc.

This comes from our mindset and how we think about situations and certain things. The mindset consists of thought processes we unconsciously acquire to avoid difficult situations or efforts. Such thought processes are also formed during our upbringing. For example, a child constantly criticized for their successes and failures will find it challenging to dare try something new. However, the lack of criticism makes the child overconfident, which can lead to misjudgment of their abilities.

A mindset can also be described as a set of different (not only culturally conditioned) beliefs. An example is a belief that eye contact is a sign of interest and openness everywhere. However, in Japan, this is considered an invasion of privacy and is considered rude.

It is advisable to be aware of such thought processes. Once we understand our own way of thinking, we have more information to work with and thus know better what we can or would like to change. For example, when we catch ourselves thinking thoughts like "I cannot," we can easily change them from bad feelings to good feelings.

The only thing we have to do is to add the word "yet."

-   I cannot do this "yet."
-   This is not for me "yet."
-   I do not understand this "yet."
-   etc.

This has the effect of stimulating our beliefs and thus the mindset to pass this obstacle.

All obstacles and feelings that prevent us from doing so are temporary. These feelings pass, but the goal remains.

Another factor often perceived as an obstacle is comparing skill, talent, and passion. However, we have already learned what constitutes talent.

-   Talent is a strongly developed skill with high efficiency.
-   Skill is the ability to manage or solve something well.
-   Passion is an emotional commitment to a particular area.

If we take a closer look at these definitions, we will see that they are interrelated and mutually supportive and not, as many believe, holding them back. We all have different talents, thought patterns that make some tasks easier to understand and others a little more complicated, skills we learn, and the passion and dedication to achieve the desired goal. All this depends on the goal we want to achieve. Not on the components that help us achieve it.

* * * * *

### Pressure
--------

Pressure can also be described as mental stress, the totality of all detectable external and internal influences. Psychological pressures affect people based on a situation. They make demands on their resources. The term "stress" therefore describes a characteristic of conditions and not characteristics of people. In contrast to the term "pressure," the term "stress" describes the non-specific reaction of the organism to any form of pressure. The occurrence of stress requires a sensory perception of the stress-triggering stimulus and a nervous transmission of such a stimulus to a stimulus-processing region of the body. Accompanying symptoms on the biochemical level are usually the release of stress hormones, such as catecholamines, glucocorticoids, and other secretions.

A distinction is made between internal and external influences. The internal influences include the beliefs of our mindsets but also our attitudes. Such an attitude or character trait is always a two-sided sword that brings advantages and disadvantages. One of such traits can be perfectionism, for example, which awakens in us the desire to do everything flawlessly, perfectly, and above all, quickly.

It is challenging to dampen such character traits because they occur unconsciously and are reflected in the form of emotions. For example, if we feel uncomfortable and overwhelmed by a task, we unconsciously think we are not up to the task. Often we also ask ourselves:

-   Why should we continue with it at all?

Since our subconscious governs it, it is necessary to put our brain into a different "mode," forcing our brain to function differently. A specific category of activity that forces our brain to behave differently is called `creativity`.

One such creative activity is making music or drawing. The reason is that we force the brain to invent something new. At the same time, we cannot focus on the mindset while developing something new as this requires completely different thought processes than dealing with a task.

If we find ourselves in a situation where we do not know what to do, we can pursue some activity requiring us to do something new. It does not matter what we do, but rather that it requires our creativity.

External influences are what others think and say about us. It can also be that strict deadlines are set for us that we must adhere to. However, it can also be that someone tries to influence us negatively. Many people do this to push their own ego, which has little to do with us and our abilities. Such people often claim to be better at something than we are. However, if we think back to our examples of the mindset we discussed earlier, we can also attach the word "yet" to these sentences and see how quickly we will overtake them.

Knowing that we only feel verbally attacked by people we attribute a high value to is essential. For example, there is a big difference between a stranger on the street calling us an "idiot" and one of our loved ones. So if we think highly of the person or their abilities, we will value their statements highly and often even place them above our own opinions. Otherwise, we care little about what that person says.

We can eliminate external influences more easily than many might think. All we need is our clearly defined goal. If we have such a goal that we follow passionately, hardly anyone will talk us out of it. It is even less likely if we know that we can achieve this goal.

We should remember the following:

-   Only the person who has taken the exact same journey as you can evaluate you and your decisions. Everything else is only assumptions.

## Questioning

* * * * *

Learning to ask the right questions is an art and a critical skill. It does not matter what situation we are in or whether we are discussing technical or non-technical topics. However, many people do not know the difference between wrong and right questions. Most do not even know what a question is. At the moment, we define questions and see their purpose as gathering information and facts from which we can draw conclusions and make assumptions that will guide our decisions and thus our future course of action. However, this opinion will soon change. Apart from that, questions often serve for orientation. By this, we mean that we can get an overview based on the questions we ask, which helps us to find more information about the topic we are concerned with. Questions represent the view of the situation before we take the next step and move on our way. Metaphorically speaking, we use them to see where we want to be or can take our next step.

Especially in our field of cyber security and above all in penetration testing, we should keep the following in mind:

`The most important and most difficult thing in any situation is not the search for the right answer but the search for the right question.`

A good example is that if an answer to a task is already known, the task is no longer necessarily difficult to solve. Many people believe that searching for an answer is one of the most difficult activities that accompany them throughout their lives. However, finding the answer becomes the opposite when the question is asked correctly. It is much more challenging to ask the right questions when we do not understand the concepts or do not have any knowledge of a particular area in the first place. We have all been in a situation where we suddenly did not know what to do and could not even understand what to start with to figure out the situation.

At this point, we should choose 3 to 5 such situations from our lives and write down one question for each of them. These can be any situation. We can take difficult and obscure situations and then write down a question for them. Throughout this section, we will learn a model that will help us see the difference between the quality of the questions we were asking and the questions we needed to ask. In doing so, we will also quickly become aware of the model's effectiveness and how much it would have helped us at the time. This is the best way to judge the effectiveness based on our personal life experiences. Therefore, we should not skip this step and write down 3 to 5 situations from our lives now.

* * * * *

### Question States
---------------

First of all, we need to solve a certain myth about questions before we continue at this point. We need to be clear about the following:

-   There are no "good" or "bad" questions. End of story.

Let us examine the following question and clear up this myth once and for all:

-   `What are "good" questions?`

Let us assume that the answer is `X`, `Y`, and `Z`. Is this question "good" or "bad"?

It does not matter and is irrelevant. "Good" or "bad" is a state we attribute to the question. What influence does this condition have on the answer? - None. The answer remains `X`, `Y`, and `Z`.

If we do something that does not affect the result, it does not matter and is therefore completely irrelevant. This is the same as asking ourselves:

-   "What happens if I jump into the water?"

To this question, we then add the following factors:

-   "The water is cold/hot/dark/transparent."

How does the water's condition affect the result when we jump into the water? - It does not. Apart from all the other consequences, we get wet either way. The interesting thing is that with the condition, we have even come closer to the actual situation. Because we used it to describe the state of the water, this is much closer connected than the state of the question. How would we influence the result if we set the state of the question and say that it is a "good" question? - We would not.

People use the states "good" and "bad" to describe the profit or loss they expect from the question. If people get an answer that benefits them, they classify the question as a "good" one. However, what if the question leads to a loss or, let us even say, does not help the person? Is the question bad? - Actually, not.

The state we give to the questions does not affect the answers. The state attributed to the question belongs to the answer or the result. The answer can be to some extent "good" or "bad," but not necessarily, depending on our goal and whether we are getting closer to it. If we come closer to the answer/result, moving away from the less ideal goal is good.

We can assign two states to a question; thus, we would describe it as a `rough question` or a `precise question`.

-   A `rough question` would be, for example, "How can I hack X?"
-   A `precise question` would be: "How can I use the server's SMB service to identify its existing user accounts?"

As we can see from these two examples, this state of precision can greatly affect the result and the answer. Nevertheless, a precise question is still not good. Because `good` or `bad` are irrelevant states, we now know that they do not influence the result or the answer.

* * * * *

### Questions in General
--------------------

We use questions in everyday life more often than we realize at first glance. On average, we ask between 3-5 questions per minute. Of course, this depends on the situation. We can experiment and set a timer for 1 minute and observe our thoughts during this period. Every time we notice that we ask ourselves something or something is unclear to us, we make a mark on a piece of paper until the timer runs out. To do this experiment, we need to take a pen and a piece of paper and set the timer. From now on, the timer should run.

Questions can be asked in many different ways. Because all questions are adapted to the circumstances, situations, and the desired goal. Questions are an essential part of the thinking process in which links are created between information nodes in our brain. Thus, it is also a fixed and unavoidable part of the learning process. Removing questions, therefore, also reduces the learning process enormously. If we do not question anything when we read content, it is like a cooking recipe without any information about how to prepare it. Because a recipe contains a big question from the ground up:

-   `How do I cook the dish?`

Two main points are worked through for each recipe:

1.  ingredients
2.  method of preparation

Learning material content can be equated with the ingredients. The preparation method can therefore be correlated with our questions because the questions determine which step we will take next and define our approach. Finally, how the cook describes the preparation method describes when, how, and what needs to be added and processed to get closer to the finished dish. The cook or author's approach may have worked 100%, but anyone who has ever cooked from a recipe knows that a written down recipe alone will not make the dish tasty.

-   We must prepare and practice it, using the means at our disposal.

A professional cook typically has considerable experience and often uses special ingredients that can be very expensive, and we do not know any other use for them. Therefore, this is an essential example that copying and imitating what has been shown and explained will not always produce the desired result.

By now, the timer should have run out, and now we should add up the number of questions that came to mind while reading during this period. For comparison, at least ten questions could have been asked. If more than ten questions came up for us, all the better. The more questions we ask, the better understanding we develop of the whole picture.

To do this, let us briefly imagine the situation where we need to open a lock and follow a methodology that most people use today. The question that can be concluded from this situation is:

-   How do we open the lock?

The question is unnecessary if it is a standard door lock because we have enough experience and knowledge to open the door with the appropriate key. In this case, the key is the known tool that we use to unlock or lock the door. The situation is different if we have a vault in front of us that requires a combination of numbers. What questions do we need to ask to get the answers that will allow us to find the right tools or methods and use them accordingly?

Once we know the goal (`The Goal`) to which we are attracted (`Willingness`), we can use various principles, such as the Pareto Principle or Occam's Razor, to develop our talents (`Talent`) and skills and make our decisions (`Decision Making`) to pass the obstacles that fall across our path by asking the right questions (`Questioning`).

We can all ask questions. However, not many know how to ask the right questions. Because some significant differences and influences can greatly affect the answers we want to receive. The goal of the question is one of the most important aspects that determine our approach and the question we ask. Let us look at a few things that we currently use in our everyday lives. Such goals that we have just talked about can be, for example:

-   To understand the reason for an event (`past`)
-   To experience something completely new and to understand the way something works (`present`)
-   to predict the effect of an event (`future`)

Every question is based on three aspects with which we build our questions every day:

1.  origin
2.  process
3.  result/goal

These questions can be of any kind and can relate to duration, reason, action/reaction, location, specification, and many others. They can be as varied as our imagination. Almost every question is based on our needs, time, type, and place.

So far, everything seems to be accurate and logical. However, it is not. At this point, a few questions arise that we need to clarify.

1.  What is a question?
2.  Regardless of the form, what purpose does a question serve?

The official definition of a question is as follows:

-   `A question is a sentence worded or expressed to elicit information.`

This definition has two core elements: `sentence` and `information`. So what is a `sentence`?

The definition of `sentence` is as follows:

-   `A sentence is a set of words that is complete in itself, typically containing a subject and predicate, conveying a statement, question, exclamation, or command, and consisting of a main clause and sometimes one or more subordinate clauses.`

Moreover, here comes the exciting part; a collision that will change many things for us.

How many words must be used to ask the shortest question?

The answer to that is `a single word`. Here are a few examples:

-   "Why?"
-   "How?"
-   "Where?"

Is it an actual question? - Yes. Is it the shortest question or one of the most straightforward questions? - Yes.

Of course, these questions need context, like any other question, but this does not exclude the fact that these questions in this form with a single word represent a real question. Thus, the official definition of a question does not fit anymore.

Next, the definition of a question explains its purpose. Therefore, according to the definition, the purpose is to obtain or acquire `information`.

Let us, therefore, create a situation with a question to test this statement. Let us assume we see `host A` and `host B`. To do this, we can ask the following question, which we will also ask during our penetration tests:

-   `How is Host A connected to Host B?`

Our goal was to obtain or acquire information with the help of the question posed. Did we obtain or acquire any information from this question? - No. Regardless of the form of the questions asked, strictly speaking, the official definition of the question also missed the point. This is an example of how we can question certain things. As we see, the effect and the surprise can make one wonder. After all, we have just discovered that the official definition does not apply to a question.

Of course, a deep discussion can be started about the question's meaning, purpose, and how it should be asked. But furthermore, here is where the question arises:

-   `How should we then define a question if the official definition does not apply?`

Here we see the global scale when the goal has been set incorrectly.

What goal could we set for ourselves if the previous goal "to obtain information" can be constantly missed?

* * * * *

### Relationship-Oriented-Questioning Model
---------------------------------------

To do this, we must consider what our questions have in common. All our questions have a commonality: the `relationship` between the individual components. So let us take a quick look at a model we have developed, which we call the `Relationship-Oriented-Questioning Model` (`ROQ`), and see how it looks and works.

![[Questioning1.png]]

This model represents five components:

| Component | Description |
| --- | --- |
| `Your Position` | This describes the position we are in and our view. |
| `The Object` | The object is the core element of the question. The main component of our sentence takes the meaning out of the question. |
| `Known` | This information is known to us. |
| `Unknown` | This information is not known to us. |
| `Other Position(s)` | This component describes the position of other persons. |

We need these components to be able to ask any question correctly. To do this, we ask any question we are interested in and break it down using the `ROQ` model. Certain aspects must be considered with this model, as with all others.

1.  We need to find out the core element of the question and insert it as the object.
2.  We must have at least two components defined in the model. More than two components are optional.

The good thing is that we always already have one component:

-   Our position in the question.

So even for questions that do not directly concern us or about situations we are not involved in, we still have a position and view on the object. So let us look at an example using the following question:

-   `What are all the methods available to remotely access Windows operating systems?`

Once we have asked our question, we can break it down into its constituent parts in the `ROQ` model:

![[Questioning2.png]]

| Component | Question Part | Description |
| --- | --- | --- |
| `Your Position` |  | Our position where we are situated. |
| `The Object` | Windows | The Object is the core element of the question. The main component of our sentence takes the meaning out of the question. |
| `Known` | Methods | This information is known to us. |
| `Unknown` | Methods | This information is not known to us. |
| `Other Position(s)` |  | This component describes the position of other persons. |

Based on the parts assigned to the components, we now have to define in which relationship they act among each other. In the graphic, we see solid and dashed lines.

-   `Solid line`: Connection - How is X connected to Y?
-   `Dashed line`: Affection - How does Y influence the state of component X?

#### Connecting the Components

With this, we can go through the individual relationships and establish them between the individual components. It is recommended to always start with the object, which in this case is the Windows operating system. First, we need to establish and understand our position on the object.

-   What is the purpose for us to use Windows?

Mainly we use the operating system to use its functions to solve our tasks. We describe this as `Operating on`.

-   How does Windows influence our state in our position?

Windows is the most used operating system in the world and has the most compatibility and many user-friendly functions. Therefore, we can also summarize this and call it `Provides functionality`.

![[Questioning3.png]]

Now we can connect the relations between Windows and the methods we know.

-   What must Windows do or offer to be managed by remote access methods?

A service must allow remote access over the Internet or network. We know for sure `WinRM`, `Remote Desktop`, and a few more. (If not, it does not matter. We will learn about these in other modules). Otherwise, we would not be able to access it remotely. We call this connection `Listening Service`.

Next, the following question comes up:

-   How do the remote access methods affect Windows and thus change the state of Windows? What do these methods provide us with?

Here the answer and the purpose are already in the description - these allow `Remote Access`.

![[Questioning4.png]]

Now let us look at what we know about the known remote access methods.

-   What is the purpose of remote access methods?

The purpose is to be able to manage Windows in different ways remotely. So all we do with it is to use it. So, therefore, we call this connection `Using`.

-   How do the different remote access methods that we know affect us?

Apart from the different services these methods are designed for, they all have one thing in common. They allow us to interact with Windows. Therefore we call this connection `Allow to interact with`.

![[Questioning5.png]]

Since we already know some remote access methods, we know how they are connected to Windows. Before Windows can be accessed remotely, the corresponding service must be running.

-   Which services must Windows have running to use methods unknown to us?

We can not know this because the methods are unknown to us. Therefore we name it like this: `???`

Now the same question arises again.

-   How do the remote access methods affect Windows and thus change the state of Windows? What do these methods offer us?

The different methods offer different ways to access Windows. Because the purpose of the methods, in this case, has not changed. Therefore we call it again: `Remote Access`.

![[Questioning6.png]]

Now that we know and understand the relationships between all the individual components, we know exactly what information we are missing and what we should focus on. In this case, we can use `Windows services` to find the unknown remote access methods. Therefore, if we look closely at all possible services that allow remote access, we can probably even find our own ways to use the service for remote access.

The special thing about this model is that it is stackable. For example, if we have identified such Windows services and found unknown methods, the field `Unknown` becomes `Known` and would look like this:

![[Questioning7.png]]

* * * * *

### Practice
--------

The model may be unusual at first, and from experience, I can say that many people have difficulties in the beginning to apply this model. You will be using this model subconsciously after practicing five to ten times. You will not have to think about it much, and you will see the difference in a very short time when you have practiced this model. In fact, with these few practice sessions, you will internalize this model so much that you will even begin to use it automatically during conversations. This is the recipe that I have given you, and now you must learn to prepare the dish yourself.

Now take the 3 to 5 questions from the situations we had to write down at the beginning of this section and apply this model. You will be amazed at the conclusions you will come to.

However, this model has one special feature. If applying this model to your question is unsuccessful, you will have to rephrase it and make it more precise. Because this feature of the `ROQ` model will not allow us to ask questions to which there is no clear answer.

Now, let us settle one last question.

-   So, what is the right question?

`A right question is a precise question that allows us to establish the relationships between the components, to understand them, and to take us one step further to the required answer.`

## Handling Frustration

---

Frustration is an emotional reaction to an event, situation, or condition that occurs in the form of disappointment or powerlessness. Most often, such a feeling occurs in varying intensity, depending on expectations or desires. There are two different types of frustration. One is caused by `external influences`, such as negative opinions of superiors, and the other is caused by `inner frustration`, caused by conscious or somewhat subconscious thought processes.

Most people are not aware that feelings `reflect subconscious thoughts` and thought processes. That is why we can understand quite well how we think from our feelings. Often it helps to listen to our thoughts from a 3rd-person perspective or imagine that our best friend expresses these thoughts. With that, we gain some distance from the feeling of being affected by it, which makes it easier to construct an objective opinion and judgment about it.

Everyone has an individual frustration tolerance, which is why people with a low frustration tolerance tend to give up or break off quickly when unexpected resistance arises, or the expected success does not occur within a specific time. The result of this behavior is an increased tendency to stress and avoidance and partly aggressive forms of reaction.

The frustration tolerance can be trained and developed very well. There have certainly been situations where we may have experienced a friend in a stressful situation who remained impressively calm. For this situation, the frustration tolerance was very pronounced. Many factors can speak for this, but the fact remains that the situation seemed to be much more stressful for us than our acquaintance let it affect him.

In order to express frustration tolerance in this way, it is crucial to know where it comes from. Let us take a look at the following diagram:

![[NEW_Vision.png]]

Since we are dealing with frustration here, we can see from the diagram that, in this case, we lack some resources that frustrate us. In information security and pentesting, these kinds of resources will often be information that we have to work with. Perhaps we have already read it several times that "`Enumeration is key`". If not, it is not bad. We will fall over it.

Since we are dealing with the offensive aspects of information security, it is essential that we can get the information by ourselves. This is a skill that must be continuously trained. We will have to deal with different services, sources, and technologies to find out how to get the information we need. The feeling of frustration with a lack of resources depends on our skill. If we do not have the necessary skills, we will feel anxiety, which brings us back to the topic of comfort and comfort zone. We should also understand the connections between the individual topics better to get back to the frustration tolerance level.

To express our frustration tolerance adequately, we need to `consciously but in a controlled way`, place ourselves in situations where a particular frustration can be assumed. It is important to note that this must be done in a controlled and conscious way. It must, therefore, be our conscious decision to deal with the upcoming situation.

To make it a little clearer, pay attention to our feelings for the following example:

>Imagine that you have to catch a train. To catch it in time, we are forced to run about 2 miles quickly. We take all excuses and changes out of the situation for this example ("Think Outside the Box") and determine that you have no other choice in this example. We will be sweaty, maybe we will even get a bit dirty and out of breath, and maybe we will even miss our train because it came too early for once.  
Furthermore, now let us change the situation a little bit and imagine that you consciously decide to leave the house too late and run fast to catch the train.

Even if we do not catch that train, our frustration level will be **much lower** than in the first example. We will no longer pay attention to the external factors we blame for not getting the train, but we will find ourselves analyzing our reactions.

Do not forget that this feeling of frustration is `temporary`. This means that when we feel frustrated, it will pass. Most people get scared and panicky at such a feeling, which leads to the fact that such people sometimes even react aggressively. They are not aware that it is a temporary feeling. Therefore, we do not need to be afraid to venture into such situations. Frustration passes, the experience we have gained through it remains.

Instead, over time, we will become calmer in reacting and dealing with such stressful situations, which in turn will strengthen our self-confidence. We can control our inner frustration. The frustration of the external factors, however, can hardly be controlled.

## Learning Progress

* * * * *

An important aspect to be considered in the learning process is `progress`. In order to see our progress, two specific states are compared, including a specific time window between the learning process. In other words, we compare our knowledge from the past with the present and try to keep track of the progress to give ourselves the confirmation that we have achieved something new.

When the point comes where we cannot give ourselves the confirmation, we look for it from others. However, no one else will be able to give us confirmation without taking the path together with us. To make it clear, let us return to the example of the mountains.

>Now let us suppose that you have gone down the mountain and have a very long and arduous way behind you. You have already passed a few stops and towns, and now after a couple of weeks, you meet another person whom you ask if you have already performed well.

This person will never be able to tell us if our performance was good or bad without having walked the path together with us. Metaphorically speaking, even if this person has already gone the same way, all the factors cannot have been the same, such as rain, thunderstorms, heat, wind, etc.

People who have been on the road for years will know how exhausting it can be and what hurdles they have to overcome. We only gain height by going uphill. Going uphill is always exhausting, and we may slip and slide a little bit down again. What is essential here is to keep moving constantly. How fast we want to reach a defined height depends entirely on our ambition. Whether we only take one step a day or ten steps a day only plays a role in the duration.

The difference here is easy to see. If you stop on the mountain and do not climb any further up, you will stay on the same spot. Look at the following mathematical example to see the difference in numbers:

>(1.00)365 = 1.00\
(1.01)365 = 37.7

Here we can already see the enormous difference, how much it makes, even if we only increase our performance by 1% per day. If we want to record our progress and write it down to look back and see how far we have already gone, you can create two lists.

##### List No. 1

>On the first list, you write down the current date and everything you know about your desired topic with all your skills with an estimated scale of 1-10. Try to make it as detailed as possible. The more detailed it is, the clearer the difference will be for you to see later. As soon as you think this list is ready, put it down or save it in a way that you will have access to it even after one year.

##### List No. 2

>The second list is written continuously. This means that as soon as you have familiarized yourself with a topic and you have learned something new for yourself, you will add it to this list. Try to learn every day, even if it takes only 10 minutes. If you want to do it more scientifically to get even better results, document the calendar weeks.

We will be amazed to see the progress we have made during this time. Above all, it will become evident to us why no one else but ourselves can tell if we have made good progress.

#### Questions

>To get the cubes back from this module, answer the following question. What is the difference between the two numbers of the learning progress mentioned above?