<script>
    import { onMount } from 'svelte';
 
    // Create an array of section data for easy binding
    const sections = [
      {
        content: [
          "We build world-class marketing sites for software startups.",
          "📱",
          "We are a tight-knit team",
          {
            type: "team",
            value: [
                {
                    src: "https://reboot.studio/ivan.jpg",
                },
                {
                    src: "https://reboot.studio/toni.jpg",
                },
                {
                    src: "https://reboot.studio/adrian.jpg",
                }
            ]
          },
          "with +7 years of experience helping founders",
          "showcase how good their products really are.",
          {
            type: "break"
          }
        ]
      },
      {
        content: ["Building great sites involves many disciplines."]
      },
      {
        content: ["Design. Engineering. Branding. Copywriting.",]
      },
      {
        content: ["Video. 3D. Interaction.", {
                type: "break"
            }]
      },
      {
        content: [
            "Pulling everything together comes at the expense of your product. Your team should never stop shipping. That's where we step in.",
            {
                type: "break"
            }
            ]
      },
      {
        content: [
            "We design and build the perfect site for your product. We move fast, while ensuring the highest level of craft, attention to detail and performance.",
            {
                type: "break"
            }
            ]
      }
    ];

    const handleScroll = ()=> {
        const scrollPosition = window.scrollY; // Current scroll position
        const documentHeight = document.documentElement.scrollHeight; // Total height of the document
        const windowHeight = window.innerHeight; // Height of the viewport

        // Calculate percentage of page scrolled
        let scrollPercentage = (scrollPosition / (documentHeight - windowHeight)) * 100;

        console.log(`Scrolled: ${scrollPercentage.toFixed(2)}%`);

        const collection = document.getElementsByClassName("candidate");
        console.log(collection.length)

        if(scrollPercentage < 7) {
            scrollPercentage = 7
        }

        let itemsToManipulate = Math.ceil(collection.length * scrollPercentage / 100)

        for(let i=0;i<collection.length;i++){
            const classNames = collection[i].className.split(" ")
            if (classNames.includes("text-candidate") ){
                if(i <= itemsToManipulate){
                    collection[i].style.opacity = 1;
                }else{
                    collection[i].style.opacity = 0.25;
                }
            } else if (classNames.includes("team-candidate") ){
                if(i <= itemsToManipulate){
                    collection[i].classList.replace('team-candidate-initial', 'team-candidate-scrolled')
                    const imgtags = collection[i].children
                    for(let i=0; i < imgtags.length; i++){
                        imgtags[i].style.width = "40px";
                    }
                }else{
                    collection[i].classList.replace('team-candidate-scrolled', 'team-candidate-initial')
                    const element = collection[i].children
                    const imgtags = element
                        for(let i=0; i < imgtags.length; i++){
                            imgtags[i].style.width = "0px";
                        }
                }
            }
        }
    }
 
    onMount(() => {
      handleScroll()
      window.addEventListener('scroll', () => {
        handleScroll()
        });
    });
  </script>
 
 <div class="container">
  <div class="content">
        {#each sections as section, i}
            {#each section.content as sentence, j}
                {#if typeof sentence === 'string'}
                    {#each sentence.split(' ') as word, k}
                        <span class="candidate text-content text-candidate">
                            {word}
                        </span>
                    {/each}
                {:else if sentence.type == "team"}
                    <span class="candidate team-candidate team-candidate-initial" style="position:relative;top:6px">
                        {#each sentence.value as member, l}
                            <img class="avatar" src={member.src} width="40px" height="40px">
                        {/each}
                    </span>
                {:else if sentence.type == "break"}
                    <br>
                    <br>
                {/if}
            {/each}
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
    width: 100%; /* or any specific width */
    white-space: normal; /* allows wrapping */
    }

    .text-candidate{
        transition: all 0.3s ease-in-out;        
    }

    .team-candidate{
        transform-origin: left;
        transition: all 1s ease-in-out;
        transition-timing-function: cubic-bezier(.16,1,1,1);
        display: inline-block;
        overflow: hidden;
        padding-left:4px;
        padding-right:5px;
    }

    .team-candidate-scrolled{
        transform: scale(1); /* Shrinks to invisible */
        opacity: 1; /* Fades out */
        visibility: visible;
    }

    .team-candidate-initial{
        transform: scale(0); /* Shrinks to invisible */
        opacity: 0; /* Fades out */
         visibility: hidden; 
    }
 
    .text-content {
      font-size: 35px;
      line-height: 1.3;
      font-weight: 400;
      display: inline-block; /* Ensures the span behaves like a block-level element, but stays inline */
      margin-right: 5px; 
      opacity: 0.25;
      padding-right:3px;
      color: rgb(35 35 35);
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
      border-radius: 50%;
      background: #E5E5E5;
      padding-left: 3px;
      padding-right:1px;
      margin-left: -5px;
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
    }
  </style>