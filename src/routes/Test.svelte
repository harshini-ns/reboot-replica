<script>
    import { onMount } from 'svelte';
 
    // Create an array of section data for easy binding
    const sections = [
      {
        isHighlighted: false,
        content: [
          "We build world-class marketing sites for software startups.",
          "📱",
          "We are a tight-knit team",
          {
            type: "team",
            text: "with +7 years of experience helping founders"
          },
          "showcase how good their products really are."
        ]
      },
      {
        isHighlighted: false,
        content: ["Building great sites involves many disciplines."]
      },
      {
        isHighlighted: false,
        content: ["Design. Engineering. Branding. Copywriting."]
      },
      {
        isHighlighted: false,
        content: ["Video. 3D. Interaction."]
      },
      {
        isHighlighted: false,
        content: ["Pulling everything together comes at the end."]
      }
    ];
 
    // Function to handle intersection for each section
    function handleIntersection(index, isIntersecting) {
      sections[index].isHighlighted = isIntersecting;
    }
 
    let sectionElements = [];
 
    onMount(() => {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          const index = sectionElements.indexOf(entry.target);
          if (index !== -1) {
            handleIntersection(index, entry.isIntersecting);
          }
        });
      }, {
        threshold: 0.5,
        rootMargin: '-10% 0px'
      });
 
      sectionElements.forEach(section => {
        observer.observe(section);
      });
 
      return () => observer.disconnect();
    });
  </script>
 
  <div class="container">
    <div class="content">
      {#each sections as section, i}
        <div 
          class="highlight-section" 
          class:highlighted={section.isHighlighted}
          bind:this={sectionElements[i]}
        >
          {#each section.content as item}
            {#if typeof item === 'string'}
              <span class="text-content">
                {item}
              </span>
            {:else if item.type === 'team'}
              <span class="team-section">
                <span class="avatars">
                  <span class="avatar"></span>
                  <span class="avatar"></span>
                  <span class="avatar"></span>
                </span>
                <span class="text-content">{item.text}</span>
              </span>
            {/if}
          {/each}
        </div>
      {/each}
    </div>
  </div>
 
  <style>
    :global(body) {
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, sans-serif;
      background: white;
      overflow-x: hidden;
    }
 
    .container {
      width: 50vw;
      margin: 0 auto;
      padding: 2rem;
    }
 
    .content {
      display: flex;
      flex-direction: column;
      padding: 15vh 0;
    }
 
    .highlight-section {
      color: #DDDDDD;
      transition: color 0.8s ease-out;
      margin-bottom: 1rem;
    }
 
    .highlight-section.highlighted {
      color: #000000;
    }
 
    .text-content {
      font-size: 3.5rem;
      line-height: 1.3;
      font-weight: 400;
      display: inline;
    }
 
    .team-section {
      display: inline-flex;
      align-items: center;
      gap: 1rem;
      margin: 0 1rem;
      vertical-align: middle;
    }
 
    .avatars {
      display: inline-flex;
      gap: 0.25rem;
    }
 
    .avatar {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      background: #E5E5E5;
    }
 
    @media (max-width: 1200px) {
      .container {
        width: 75vw;
      }
    }
 
    @media (max-width: 768px) {
      .container {
        width: 90vw;
        padding: 1rem;
      }
 
      .text-content {
        font-size: 2rem;
      }
 
      .avatar {
        width: 40px;
        height: 40px;
      }
    }
  </style>