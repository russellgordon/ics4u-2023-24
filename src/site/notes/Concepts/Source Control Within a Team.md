---
{"dg-publish":true,"permalink":"/concepts/source-control-within-a-team/","dgShowToc":true}
---

# Working on Issues in a Team

## Overview

There are several models for organizing source control usage within a team.

The model we will use for projects this year can be summarized as the "fork and branch" model.

Only the project manager – Mr. Gordon for the teacher-led projects we are authoring now – has write access to the primary repository for a project. The repository for a project will always be created within the **lcs-apps** organization on GitHub.

At the outset of a project, team members create *forks* of the primary repository. 

Within a repository for a project, there are two primary branches active at all times:

- `main` branch
	- Stable version of the software
- `development` branch
	- In-progress version of the software working toward a release
	- All *issue branches* are created from this branch

When a team member is ready to start working on an issue, they create an *issue branch* off of the `development` branch in their own fork of the repository.

For example, a team member working on issue 23 will create a branch named `issue23` off of `development`. They will commit and push all work on that issue to the `issue23` branch. Only code commits related to issue 23 are to be made on this branch.

> [!IMPORTANT]
> 
> **Never mix code from multiple issues within a single branch.**

When the team member is finished working on an issue, they will create a *pull request* which the project manager will review and merge into the `development` branch of the primary repository.

Visually, working on issue branches that are merged into the `development` branch of a project looks like this:

![Screenshot 2024-01-26 at 8.18.49 AM.png|500](/img/user/Media/Screenshot%202024-01-26%20at%208.18.49%E2%80%AFAM.png)

After a pull request is accepted and merged into the `development` branch of the primary project repository, the team member in question must then update the `development` branch of their own fork on [GitHub.com](https://github.com). This will pick up their changes that were just accepted into the `development` branch of the primary repository – *as well as code for issues worked on by other members of the team*.

The team member must then pull the changes from their remote to their local copy of the repository, and begin working on their next assigned issue.

> [!TIP]
> 
> Don't worry if you don't immediately understand this model for using source control! 
> 
> That would be *entirely normal*.
> 
> You will get used to it quickly – we *learn by doing* and you can ask for help whenever you need it.

## Detailed steps

1. At the outset of your participation in a project, you will create a fork of the primary project repository. You will then clone your fork to your computer. 
   
2. Going forward, when you are ready to start working on a new issue... first ensure that you are on the `development` branch in Xcode:
   
   ![Screenshot 2023-01-16 at 6.38.40 AM.png|300](/img/user/Media/Screenshot%202023-01-16%20at%206.38.40%20AM.png)
   
   If you are not, switch to the `development` branch:
   
   ![Screenshot 2023-01-16 at 6.41.55 AM.png|350](/img/user/Media/Screenshot%202023-01-16%20at%206.41.55%20AM.png)

2. Visit the GitHub remote for your fork:
   
   ![Screenshot 2023-01-16 at 7.24.13 PM.png|400](/img/user/Media/Screenshot%202023-01-16%20at%207.24.13%20PM.png)
   
   Then **sync** your fork with the primary copy of the repository to pick up recent changes:
   
   ![Screenshot 2023-01-16 at 7.26.22 PM.png|600](/img/user/Media/Screenshot%202023-01-16%20at%207.26.22%20PM.png)
   
3. Back in Xcode, pull from your fork's remote to get latest changes on the `development` branch:
   
   ![Screenshot 2024-01-26 at 8.47.46 AM (3).png|250](/img/user/Media/Screenshot%202024-01-26%20at%208.47.46%E2%80%AFAM%20(3).png)
   
   ![Screenshot 2023-01-16 at 6.44.22 AM.png|375](/img/user/Media/Screenshot%202023-01-16%20at%206.44.22%20AM.png)
   
4. Create a local branch from `development` based on your issue number.
	- For example, if your issue is [90](https://github.com/lcs-apps/Chicago-HSE-LCS/issues/90), branch name should be `issue90`.
	  
	  ![Screenshot 2023-01-16 at 6.48.08 AM.png|400](/img/user/Media/Screenshot%202023-01-16%20at%206.48.08%20AM.png)
	  
	  ![Screenshot 2023-01-16 at 6.50.20 AM.png|375](/img/user/Media/Screenshot%202023-01-16%20at%206.50.20%20AM.png)

   > [!TIP]
   > After creating or switching to a different branch, Xcode may show the marker `(current)` on two branches at the same time, which is impossible.
   > 
   > ![Screenshot 2023-01-16 at 7.01.45 AM.png|200](/img/user/Media/Screenshot%202023-01-16%20at%207.01.45%20AM.png)
   > 
   > This is a bug. To workaround this display issue, go to the Project navigator using the **Command-1** keyboard shortcut, then back to the Source Control navigator using the **Command-2** keyboard shortcut.
   > 
   > ![Screenshot 2023-01-16 at 7.04.12 AM.png|200](/img/user/Media/Screenshot%202023-01-16%20at%207.04.12%20AM.png)
   
5. Commit and push to the `issue90` branch as you work on the issue.
   
   The first time you push a commit, a remote branch will be created.
   
   ![Screenshot 2023-01-16 at 6.52.38 AM.png](/img/user/Media/Screenshot%202023-01-16%20at%206.52.38%20AM.png)
   
6. When you are finished working on the issue, go to your fork on GitHub:
   
   ![Screenshot 2023-01-16 at 7.06.45 AM.png|400](/img/user/Media/Screenshot%202023-01-16%20at%207.06.45%20AM.png)
   
   ... then initiate a pull request:
   
   ![Screenshot 2023-01-16 at 7.08.26 AM.png|600](/img/user/Media/Screenshot%202023-01-16%20at%207.08.26%20AM.png)
   
   On GitHub, describe what you have accomplished briefly (1), provide more details if necessary (2), reference the issue number (3), and then ==be certain== you are requesting a pull to the `development` branch (4):
   
   ![Screenshot 2023-01-16 at 7.12.02 AM.png](/img/user/Media/Screenshot%202023-01-16%20at%207.12.02%20AM.png)
   
   Finally, actually create the pull request (5).
   
7. In Xcode, switch back to the `development`  branch and return to step 1 of these instructions to continue working on your next issue.