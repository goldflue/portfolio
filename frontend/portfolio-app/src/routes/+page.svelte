<script lang="ts">
    import { fade, fly, type TransitionConfig } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
    import { Badge } from '@/components/ui/badge';
    import { Tooltip } from '@/components/ui/tooltip';
    import { Card, CardHeader, CardContent, CardTitle, CardDescription } from '@/components/ui/card';
    // import Header from '@/components/ui/header/header.svelte';
    import BackgroundBoxes from '@/components/ui/background-boxes/background-boxes.svelte';
    let activeSection: string = 'about';
  
    const inConfig = {
        duration: 500, 
        delay: 500
    } as TransitionConfig;

    const outConfig = {
        duration: 200, 
        easing: quintOut 
    } as TransitionConfig;

    function handleLinkClick(sectionId: string) {
      activeSection = sectionId;
    }
  </script>
  
  <style>
    /* Styles for the fixed table of contents */
    .table-of-contents {
      position: fixed;
      top: 20%;
      left: 0;
      background: var(--background, #fff);
      padding: 1rem;
      border-right: 1px solid var(--border-color, #ccc);
      width: 150px;
      z-index: 1000;
    }
  
    .table-of-contents a {
      display: block;
      margin-bottom: 1rem;
      color: var(--text-color, #333);
      text-decoration: none;
      font-weight: bold;
    }
  
    .table-of-contents a.active {
      color: var(--primary-color, #007BFF);
    }
  
    /* Adjust main content margin to accommodate the table of contents */
    main {
      margin-left: 160px; /* Adjust according to the width of the table of contents */
    }
  
    /* Responsive design */
    @media (max-width: 768px) {
      .table-of-contents {
        position: static;
        width: 100%;
        border-right: none;
        border-bottom: 1px solid var(--border-color, #ccc);
        display: flex;
        justify-content: center;
        padding: 0.5rem;
      }
  
      .table-of-contents a {
        margin: 0 1rem;
      }
  
      main {
        margin-left: 0;
      }
    }
  </style>

  <div class="flex flex-col min-h-screen">
    <!-- Fixed Table of Contents -->
    <nav class="table-of-contents">
      <a
        href=""
        on:click|preventDefault="{() => handleLinkClick('about')}"
        class:active="{activeSection === 'about'}"
        aria-current="{activeSection === 'about' ? 'page' : undefined}"
      >

        About
      </a>
      <a
        href=""
        on:click|preventDefault="{() => handleLinkClick('experience')}"
        class:active="{activeSection === 'experience'}"
        aria-current="{activeSection === 'experience' ? 'page' : undefined}"
      >

        Experience
      </a>
      <a
        href=""
        on:click|preventDefault="{() => handleLinkClick('projects')}"
        class:active="{activeSection === 'projects'}"
        aria-current="{activeSection === 'projects' ? 'page' : undefined}"
      >
        Projects
      </a>
    </nav>
  
    <!-- Main Content -->
    <main class="flex-1">
    <BackgroundBoxes />
      {#if activeSection === 'about'}
        <!-- About Section -->
        <section
          id="about"
          class="py-12 md:py-24 lg:py-32"
          in:fade={inConfig}
          out:fade={outConfig}
        >
          <div class="container px-4 md:px-6">
            <div class="grid gap-6 md:grid-cols-2 lg:gap-12">
              <div>
                <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl md:text-5xl">About Me</h2>
                <p class="mt-4 text-muted-foreground md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed">
                  I am a passionate software engineer with a strong background in full-stack web development. I love
                  creating innovative and user-friendly applications that solve real-world problems.
                </p>
              </div>
              <div class="flex flex-col gap-4">
                <div>
                  <h3 class="text-lg font-bold">Skills</h3>
                  <div class="mt-2 flex flex-wrap gap-2">
                    <Badge>React</Badge>
                    <Badge>Node.js</Badge>
                    <Badge>TypeScript</Badge>
                    <Badge>SQL</Badge>
                    <Badge>Git</Badge>
                    <Badge>Docker</Badge>
                  </div>
                </div>
                <div>
                  <h3 class="text-lg font-bold">Interests</h3>
                  <div class="mt-2 flex flex-wrap gap-2">
                    <Badge>Coding</Badge>
                    <Badge>Reading</Badge>
                    <Badge>Traveling</Badge>
                    <Badge>Photography</Badge>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>
      {:else if activeSection === 'experience'}
        <!-- Experience Section -->
        <section
          id="experience"
          class="py-12 md:py-24 lg:py-32"
          in:fade={inConfig}
          out:fade={outConfig}
        >
          <div class="container px-4 md:px-6">
            <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl md:text-5xl">Experience</h2>
            <div class="mt-8 grid gap-8">
              <div>
                <h3 class="text-lg font-bold">Software Engineer</h3>
                <div class="text-muted-foreground">Acme Inc. | Jan 2020 - Present</div>
                <p class="mt-2 text-muted-foreground">
                  Developed and maintained complex web applications using React, Node.js, and PostgreSQL. Collaborated
                  with cross-functional teams to deliver high-quality software solutions.
                </p>
              </div>
              <div>
                <h3 class="text-lg font-bold">Intern</h3>
                <div class="text-muted-foreground">Globex Corporation | Jun 2019 - Dec 2019</div>
                <p class="mt-2 text-muted-foreground">
                  Participated in the development of a customer relationship management (CRM) system using Angular and
                  Firebase. Contributed to the implementation of new features and bug fixes.
                </p>
              </div>
            </div>
          </div>
        </section>
      {:else if activeSection === 'projects'}
        <!-- Projects Section -->
        <section
          id="projects"
          class="py-12 md:py-24 lg:py-32"
          in:fade={inConfig}
          out:fade={outConfig}
        >
          <div class="container px-4 md:px-6">
            <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl md:text-5xl">Projects</h2>
            <div class="mt-8 grid gap-8 md:grid-cols-2 lg:grid-cols-3">
              <Tooltip>
                <a href="#">
                  <Card class="group relative overflow-hidden rounded-lg shadow-lg transition-all duration-300 hover:scale-105 hover:shadow-2xl">
                    <CardHeader>
                      <img
                        src="/placeholder.svg"
                        alt="Todo App"
                        width="600"
                        height="400"
                        class="w-full h-48 object-cover group-hover:opacity-80 transition-opacity duration-300"
                        style="aspect-ratio: 600/400; object-fit: cover;"
                      />
                    </CardHeader>
                    <CardContent>
                      <CardTitle>Todo App</CardTitle>
                      <CardDescription>
                        A simple and intuitive todo list application built with React and Firebase.
                      </CardDescription>
                      <div class="flex items-center gap-2 mt-4">
                        <Badge>React</Badge>
                        <Badge>Firebase</Badge>
                      </div>
                    </CardContent>
                  </Card>
                </a>
              </Tooltip>
              <!-- Add more project cards as needed -->
            </div>
          </div>
        </section>
      {/if}
    </main>
  </div>
  