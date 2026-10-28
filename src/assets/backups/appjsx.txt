import { useEffect, useRef, useState } from "react";

import { motion, AnimatePresence } from "framer-motion";

import "./App.css";




const tabs = ["About", "Work", "Interests"];



const projects = [
  {
    id: "whatsapp",
    title: "WhatsApp Redesign",
    type: "UX Case Study",
    category: "UI/UX",
    year: "2026",
    description:
      "Reimagining the chat experience to separate personal conversations from everyday clutter.",
    visual: "visual-ux",
    image: "/images/projects/whatsapp-redesign.png",
    link: "https://medium.com/@officialamogh49/redesigning-whatsapps-chats-screen-giving-business-messages-a-home-of-their-own-e1e2d283c976?sharedUserId=officialamogh49",
  },
  {
  id: "college-website",
  title: "Reimagining College Website",
  type: "Web Design",
  category: "Web Design",
  year: "2026",
  description:
    "A refreshed college website focused on clearer navigation, better hierarchy, and usability.",
  visual: "visual-web",
  image: "/images/projects/college-website.png",

  caseStudy: "/pdfs/Case_Study.pdf",
  prototype: "https://www.figma.com/proto/Ohe5tz2hFCTLsG2VuCgrDz/Intern?node-id=397-1306&t=38b853cwVBqbFthf-1&scaling=min-zoom&content-scaling=fixed&page-id=224%3A643&starting-point-node-id=397%3A1306",
},
  {
    id: "focusflow",
    title: "FocusFlow",
    type: "Product Design",
    category: "UI/UX",
    year: "2026",
    description:
      "A productivity workspace designed to make planning and focus feel effortless.",
    visual: "visual-product",
    image: "/images/projects/focusflow.png",
    link: "https://focus-flow-lovat-one.vercel.app/",
  },
];


const graphicWorks = [
  // ARTWORKS
  {
    id: "affinity-poster",
    title: "Affinity Poster",
    image: "/images/graphic-design/artworks/affinity poster.png",
    description: "Just a simple poster made in Affinity Designer. Affinity launched its free creative suite as a direct competitor to Adobe, and honestly, it’s surprisingly good. Had to give it a try!",
    group: "Artwork",
  },
  {
    id: "billu-fashion-cat",
    title: "Billu Fashion Cat",
    image: "/images/graphic-design/artworks/billu-fashion cat.png",
    description: "Created this poster imagining cats as models as they have that attitude, and just designing to express and experiment.",
    group: "Artwork",
  },
  {
    id: "genz-artwork",
    title: "Gen Z Artwork",
    image: "/images/graphic-design/artworks/genz artwork.png",
    description: "Created a y2k aesthetic poster as i was inspired from the posters and brand early creative posters, such as Sony, Nokia and many..",
    group: "Artwork",
  },
  {
    id: "interesting-artwork",
    title: "Interesting Artwork",
    image: "/images/graphic-design/artworks/Intresting artwork.png",
    description: "I was looking this youtube video of creator named olgaloiek who said this quote which goes like ~Being interested is being intresting and really liked the quote and i had to create something of my own.",
    group: "Artwork",
  },
  {
    id: "kinetic-soundwave",
    title: "Kinetic Soundwave Nights Poster",
    image: "/images/graphic-design/artworks/Kinetic Soundwave Nights Poster.png",
    description: "Just a chatgpt challenge to create a poster for a event",
    group: "Artwork",
  },
  {
    id: "touchgrass",
    title: "Touchgrass",
    image: "/images/graphic-design/artworks/touchgrass.png",
    description: "This one was inspired by the phrase “Touch Grass,” used by Gen Z to tell someone to step away from their screens and go outside for a while. Then I started imagining how people often end up getting work from their bosses even during vacations. So, how does one touch grass when they can’t even escape work, even if they wanted to?",
    group: "Artwork",
  },
  {
    id: "why-are-you-gay",
    title: "Why Are You Gay?",
    image: "/images/graphic-design/artworks/why are you gay.png",
    description: "Just imagined how would it be a poster of a meme, and No i am not gay lol",
    group: "Artwork",
  },

  // CLIENT WORK
  {
    id: "cleanup-drive",
    title: "Cleanup Drive",
    image: "/images/graphic-design/clientwork/cleanup drive.png",
    description: "Designed a poster and carousel like post to cleanup drive in my city out of giving something back to society as help.",
    group: "Client Work",
  },
  {
    id: "clinic-banner",
    title: "Clinic Banner",
    image: "/images/graphic-design/clientwork/clinic banner final.png",
    description: "Designed a clinic banner for a pediatrician.",
    group: "Client Work",
  },
  {
    id: "bankruptcy-cover",
    title: "Cover Bankruptcy",
    image: "/images/graphic-design/clientwork/Cover-Bankruptcy.png",
    description: "Helped a friend at IICA design a cover page for his project.",
    group: "Client Work",
  },
 
  {
    id: "davana-logo-2",
    title: "Davana Event Logo 2",
    image: "/images/graphic-design/clientwork/Davana Event logo2.png",
    description: "Logo designed for my college fest",
    group: "Client Work",
  },
  
  {
    id: "dish-bakes",
    title: "Dish Bakes",
    image: "/images/graphic-design/clientwork/dish bakes.png",
    description: "Helped my friend kickstart her cake business with a few designs.",
    group: "Client Work",
  },
  {
    id: "invincible-thumbnail",
    title: "Invincible Thumbnail Design",
    image: "/images/graphic-design/clientwork/Invincible thumbnail design.png",
    description: "Designed a thumbnail for as a part of practicing and experimentation",
    group: "Client Work",
  },
  {
    id: "karawali-kai-ruchi",
    title: "Karawali Kai Ruchi",
    image: "/images/graphic-design/clientwork/karawali kai ruchi.png",
    description: "Designed this menu card for a food festival at my University",
    group: "Client Work",
  },
  {
    id: "opal-salon",
    title: "Opal Salon Poster",
    image: "/images/graphic-design/clientwork/opal salon poster.png",
    description: "Designed a promotional banner for the storefront of my client's unisex spa.",
    group: "Client Work",
  },
];



function App() {
  const [showAllGraphicWorks, setShowAllGraphicWorks] = useState(false);
  const [activeTab, setActiveTab] = useState("About");
  const [toolPage, setToolPage] = useState(0);
  const [activeFilter, setActiveFilter] = useState("All");
  const [selectedWork, setSelectedWork] = useState(null);
  const [selectedProject, setSelectedProject] = useState(null);
  useEffect(() => {
  if (!selectedWork) return;

  const handleKeyDown = (event) => {
    if (event.key === "Escape") {
      setSelectedWork(null);
    }
  };

  document.addEventListener("keydown", handleKeyDown);

  return () => {
    document.removeEventListener("keydown", handleKeyDown);
  };
}, [selectedWork]);


  const heroRef = useRef(null);

const roles = [

  "Graphic Designer",

  "UI/UX Designer",

  "Wed Designer",

  "Vibe Coder", 

];

const tools = [
  { name: "Figma", image: "figma.png", level: 8 },
  { name: "Photoshop", image: "photoshop.png", level: 6 },
  { name: "Illustrator", image: "illustrator.png", level: 4 },
  { name: "Affinity Designer", image: "affinity-designer.png", level: 6 },
  { name: "Canva", image: "canva.png", level: 8 },
  { name: "Webflow", image: "webflow.png", level: 6 },
  { name: "VS Code", image: "VS Code.png", level: 8 },
  { name: "HTML & CSS", image: "html5.svg", level: 8 },
  { name: "JavaScript", image: "javascript.svg", level: 6 },
];



const toolsPerPage = 6;
const totalToolPages = Math.ceil(tools.length / toolsPerPage);

const visibleTools = tools.slice(
  toolPage * toolsPerPage,
  (toolPage + 1) * toolsPerPage
);

const [roleIndex, setRoleIndex] = useState(0);

useEffect(() => {

  const interval = setInterval(() => {

    setRoleIndex((prev) => (prev + 1) % roles.length);

  }, 2200);

  return () => clearInterval(interval);

}, []);


useEffect(() => {
  const hero = heroRef.current;
  if (!hero) return;
  const images = Array.from(

    hero.querySelectorAll(".trail-image")

  );

  const trail = images.map(() => ({
    x: window.innerWidth / 2,
    y: window.innerHeight / 2,
    targetX: window.innerWidth / 2,
    targetY: window.innerHeight / 2,
    rotation: 0,
    targetRotation: 0,
    visible: false,
  }));

  let mouseX = 0;
  let mouseY = 0;
  let lastSpawnX = 0;
  let lastSpawnY = 0;
  let imageIndex = 0;
  let imageOrder = [];
  let lastSpawnTime = 0;
  let animationFrame;

  const shuffle = () => {
    imageOrder = Array.from(
      { length: 26 },
      (_, i) => i + 1
    ).sort(() => Math.random() - 0.5);
  };
  shuffle();
  const handleMouseMove = (event) => {
    const rect = hero.getBoundingClientRect();

    mouseX = event.clientX - rect.left;
    mouseY = event.clientY - rect.top;
    const distance = Math.hypot(
      mouseX - lastSpawnX,
      mouseY - lastSpawnY
    );
    const now = performance.now();
    if (distance < 80 || now - lastSpawnTime < 100) {
      return;
    }



    lastSpawnX = mouseX;

    lastSpawnY = mouseY;

    lastSpawnTime = now;



    if (imageIndex >= imageOrder.length) {

      shuffle();

      imageIndex = 0;

    }



    const slot = imageIndex % images.length;

    const image = images[slot];

    const item = trail[slot];



    const selectedImage = imageOrder[imageIndex];



    imageIndex++;



    item.targetX = mouseX;

    item.targetY = mouseY;



    item.targetRotation =

      (Math.random() - 0.5) * 18;



    item.visible = true;



    image.src =

      `/images/interest${selectedImage}.jpeg`;



    image.classList.add("is-visible");



    clearTimeout(item.hideTimer);



    item.hideTimer = setTimeout(() => {

      item.visible = false;

      image.classList.remove("is-visible");

    }, 1400);

  };



  const handleMouseLeave = () => {

    trail.forEach((item, index) => {

      item.visible = false;

      images[index].classList.remove(

        "is-visible"

      );

    });

  };



  const animate = () => {

    let previousX = mouseX;

    let previousY = mouseY;



    trail.forEach((item, index) => {

      const easing = index === 0 ? 0.14 : 0.10;



      if (index === 0) {

        item.targetX = mouseX;

        item.targetY = mouseY;

      } else {

        const previous = trail[index - 1];



        item.targetX = previous.x;

        item.targetY = previous.y;

      }



      item.x +=

        (item.targetX - item.x) * easing;



      item.y +=

        (item.targetY - item.y) * easing;



      item.rotation +=

        (item.targetRotation - item.rotation) *

        0.08;



      const image = images[index];


      image.style.transform = `

        translate3d(

          ${item.x}px,

          ${item.y}px,

          0

        )

        translate(-50%, -50%)

        rotate(${item.rotation}deg)

      `;



      previousX = item.x;

      previousY = item.y;

    });



    animationFrame =

      requestAnimationFrame(animate);

  };



  hero.addEventListener(

    "mousemove",

    handleMouseMove

  );



  hero.addEventListener(

    "mouseleave",

    handleMouseLeave

  );



  animationFrame =

    requestAnimationFrame(animate);



  return () => {

    hero.removeEventListener(

      "mousemove",

      handleMouseMove

    );



    hero.removeEventListener(

      "mouseleave",

      handleMouseLeave

    );



    cancelAnimationFrame(animationFrame);



    trail.forEach((item) => {

      clearTimeout(item.hideTimer);

    });

  };

}, []);



  return (

    <main>

      <nav className="top-nav">
  <a href="#" className="nav-brand" aria-label="Amogh Design home">
    <img src="/amoghdes.png" alt="Amogh mascot" className="nav-mascot" />
  </a>

  <a
    className="nav-email"
    href="https://mail.google.com/mail/?view=cm&fs=1&to=officialamogh49@gmail.com"
    target="_blank"
    rel="noopener noreferrer"
  >
    Email Me ↗
  </a>
</nav>

      <section

        className="hero"

        ref={heroRef}

      >

        <div className="hero-trail">

          {[0, 1, 2, 3, 4].map((index) => (

            <img

              key={index}

              className="trail-image"

              src="/images/interest1.jpeg"

              alt=""

            />

          ))}

        </div>



        <motion.div

          className="hero-content"

          initial={{

            opacity: 0,

            y: 40,

          }}

          animate={{

            opacity: 1,

            y: 0,

          }}

          transition={{

            duration: 1,

            ease: [0.22, 1, 0.36, 1],

          }}

        >

          <div className="hero-content">

  <p

  className={`hero-role role-${roleIndex}`}

  key={roleIndex}

>

  {roles[roleIndex]}

</p>







  <h1>

    AMOGH

    <br />

    PUTHANIKAR

  </h1>



  <p className="hero-copy">

    Multidisciplinary designer I blend graphic design, user-centered thinking (UI/UX) and code

    to create thoughtful digital experiences.

  </p>

</div>

        </motion.div>

      </section>

{/* WORK SECTION */}

<section className="work-section" id="work">
  <div className="work-heading">
    <div>
      <span className="work-eyebrow">WORK</span>
      <h2>Things I've made.</h2>
    </div>

    <p>
      A collection of interfaces, visual identities, websites, and creative
      experiments shaped by curiosity.
    </p>
  </div>

  <div className="work-filters">
    {["All", "UI/UX", "Graphic Design", "Web Design", "Experiments"].map(
      (filter) => (
        <button
          key={filter}
          type="button"
          className={`work-filter ${
            activeFilter === filter ? "active" : ""
          }`}
          onClick={() => setActiveFilter(filter)}
        >
          {filter}
        </button>
      )
    )}
  </div>

  <div className="work-grid">
    {/* EXISTING PROJECT CARDS */}
    {projects
      .filter(
        (project) =>
          activeFilter === "All" || project.category === activeFilter
      )
      .map((project, index) => (
        <motion.article
          className="work-card"
          key={project.id}
          initial={{ opacity: 0, y: 18 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true, amount: 0.15 }}
          transition={{
            duration: 0.45,
            delay: index * 0.06,
            ease: [0.22, 1, 0.36, 1],
          }}
          whileHover={{ y: -5 }}
        >
          <div className="work-card-content">
  <a
    className="work-card-link"
    href={project.link || project.prototype || undefined}
    onClick={(event) => {
      if (!project.link && !project.prototype) {
        event.preventDefault();
      }
    }}
    target={project.link || project.prototype ? "_blank" : undefined}
    rel="noreferrer"
    aria-label={`View ${project.title}`}
  >
    <div className="work-card-image">
      <img
        src={project.image}
        alt={project.title}
        loading="lazy"
        onError={(event) => {
          event.currentTarget.style.display = "none";
        }}
      />

      <span className="work-card-number">
        {String(index + 1).padStart(2, "0")}
      </span>

      <span className="work-card-arrow">↗</span>
      {/* PROJECT LINKS OVER IMAGE */}
{(project.caseStudy || project.prototype) && (
  <div className="work-card-overlay">
    {project.caseStudy && (
      <a
        href={project.caseStudy}
        target="_blank"
        rel="noreferrer"
        className="work-card-overlay-btn"
        onClick={(event) => event.stopPropagation()}
      >
        View Case Study ↗
      </a>
    )}

    {project.prototype && (
      <a
        href={project.prototype}
        target="_blank"
        rel="noreferrer"
        className="work-card-overlay-btn"
        onClick={(event) => event.stopPropagation()}
      >
        View Prototype ↗
      </a>
    )}
  </div>
)}
    </div>

    <div className="work-card-info">
      <div>
        <span className="work-card-category">
          {project.category} / {project.year}
        </span>
        <h3>{project.title}</h3>
      </div>

      <span className="work-card-type">{project.type}</span>
    </div>

    <p className="work-card-description">
      {project.description}
    </p>
  </a>

  {/* CASE STUDY & PROTOTYPE LINKS */}
  {(project.caseStudy || project.prototype) && (
    <div className="work-card-actions">
      {project.caseStudy && (
        <a
          href={project.caseStudy}
          target="_blank"
          rel="noreferrer"
          className="work-card-action"
        >
          View Case Study ↗
        </a>
      )}

      {project.prototype && (
        <a
          href={project.prototype}
          target="_blank"
          rel="noreferrer"
          className="work-card-action"
        >
          View Prototype ↗
        </a>
      )}
    </div>
  )}
</div>
        </motion.article>
      ))}

    {/* GRAPHIC DESIGN ARTWORKS */}
    {(activeFilter === "All" || activeFilter === "Graphic Design") &&
      (activeFilter === "All" && !showAllGraphicWorks
        ? graphicWorks.slice(0, 6)
        : graphicWorks
      ).map((work, index) => (
        <motion.article
          className="graphic-tile"
          key={work.id}
          initial={{ opacity: 0, y: 12 }}
          whileInView={{ opacity: 1, y: 0 }}
          viewport={{ once: true, amount: 0.1 }}
          transition={{
            duration: 0.3,
            delay: (index % 4) * 0.04,
          }}
        >
          <div className="graphic-tile-image">
            <img
              src={work.image}
              alt={work.title}
              loading="lazy"
              onError={(event) => {
                event.currentTarget.style.display = "none";
              }}
            />

            <div className="graphic-info">
              <button
                type="button"
                className="graphic-info-button"
                aria-label={`Information about ${work.title}`}
                aria-describedby={`description-${work.id}`}
              >
                i
              </button>

              <div
                className="graphic-info-tooltip"
                id={`description-${work.id}`}
                role="tooltip"
              >
                {work.description || "Description coming soon."}
              </div>
            </div>
          </div>

          <div className="graphic-tile-caption">
            <h3>{work.title}</h3>
            <span>{work.group}</span>
          </div>
        </motion.article>
      ))}
  </div>

  {/* VIEW MORE BUTTON */}
  {activeFilter === "All" &&
    graphicWorks.length > 6 &&
    !showAllGraphicWorks && (
      <button
        type="button"
        className="graphic-view-more"
        onClick={() => setShowAllGraphicWorks(true)}
      >
        View all graphic works <span>↗</span>
      </button>
    )}

  {/* EMPTY STATE */}
  {projects.filter(
    (project) =>
      activeFilter === "All" || project.category === activeFilter
  ).length === 0 &&
    !(activeFilter === "Graphic Design" && graphicWorks.length > 0) &&
    activeFilter !== "All" && (
      <p className="work-empty">More projects coming soon.</p>
    )}
</section>

<section className="about-profile" id="about">

  <div className="about-intro">

    <p className="about-eyebrow">A LITTLE ABOUT ME</p>



    <h2>

      Design meets logic.

      <br />

      <span>And a little curiosity.</span>

    </h2>



    <p className="about-bio">

      I'm Amogh, a multidisciplinary designer with a

      background in Computer Science and Engineering.

      I combine graphic design, UI/UX and web development

      to create thoughtful digital experiences. I enjoy

      exploring visual ideas, experimenting with tools,

      and turning everyday observations into meaningful

      design. I'm working towards becoming a Product

      Designer, one project at a time.

    </p>



    <div className="about-facts">

      <div>

        <span>MY BACKGROUND</span>

        <p>Computer Science</p>

      </div>



      <div>

        <span>MY APPROACH</span>

        <p>Design + Technology</p>

      </div>

    </div>



    <div className="about-tools">



<div className="about-subheading toolkit-heading">

  <div className="toolkit-title-row">

    <h3>My toolkit</h3>



    <div className="xp-info">

      <button

        type="button"

        className="xp-info-trigger"

        aria-label="Explain XP bars"

        aria-describedby="xp-info-tooltip"

      >

        <span>i</span>

      </button>



      <div className="xp-info-tooltip" id="xp-info-tooltip" role="tooltip">

  <p>

    Each block represents 2 points on a 10-point proficiency scale.

  </p>



  <div className="proficiency-example">

    <span>6 / 10</span>



    <div className="proficiency-blocks" aria-hidden="true">

      {[1, 2, 3, 4, 5].map((block) => (

        <span

          key={block}

          className={block <= 3 ? "filled" : ""}

        />

      ))}

    </div>

  </div>

</div>

    </div>

  </div>



  <p>The tools behind my ideas</p>

</div>







<div className="tool-carousel">
  <div className="tool-grid">
   {visibleTools.map((tool) => (
  <div className="tool-item" key={tool.name}>
    <img
      className="tool-icon"
      src={`/images/tools/${tool.image}`}
      alt=""
      onError={(e) => {
        e.currentTarget.style.display = "none";
      }}
    />

    <div className="tool-details">
      <span className="tool-name">{tool.name}</span>

      <div
        className="proficiency-blocks"
        role="img"
        aria-label={`Proficiency: ${tool.level} out of 10`}
      >
        {Array.from({ length: 5 }, (_, index) => (
          <span
            key={index}
            className={
              tool.level >= (index + 1) * 2 ? "filled" : ""
            }
          />
        ))}
      </div>
    </div>
  </div>
))}
  </div>

  {totalToolPages > 1 && (
    <div className="tool-pagination" aria-label="Tool pages">
      {Array.from({ length: totalToolPages }, (_, index) => (
        <button
          key={index}
          type="button"
          className={`tool-dot ${toolPage === index ? "active" : ""}`}
          onClick={() => setToolPage(index)}
          aria-label={`Show tool page ${index + 1}`}
          aria-current={toolPage === index ? "page" : undefined}
        />
      ))}
    </div>
  )}
</div>



    </div>

  </div>



  <div className="about-visuals">

    <div className="about-collection">

      <div className="about-subheading">

        <h3>What I do</h3>

        <p>A mix of creativity and problem-solving</p>

      </div>



      <div className="about-illustrations">

        {[

          {

            title: "Graphic Design",

            image: "skill-graphic-design.jpeg",

          },

          {

            title: "UI/UX Design",

            image: "skill-ux-design.png",

          },

          {

            title: "Photography",

            image: "skill-photography.png",

          },

          {

            title: "Web Design",

            image: "skill-web-design.jpeg",

          },

        ].map((skill) => (

          <div className="about-illustration" key={skill.title}>

            <div className="illustration-image">

              <img

                src={`/images/about/${skill.image}`}

                alt={skill.title}

                loading="lazy"

              />

            </div>

            <h4>{skill.title}</h4>

          </div>

        ))}

      </div>

    </div>



    <div className="about-collection about-interests">

      <div className="about-subheading">

        <h3>Currently curious </h3>

        <p>Things I love exploring</p>

      </div>



      <div className="about-illustrations interests-grid">

        {[

          {

            title: "Product Design",

            image: "interest-product-design.png",

          },

          {

            title: "Motion Graphics",

            image: "interest-motion-graphics.jpeg",

          },

        ].map((interest) => (

          <div className="about-illustration" key={interest.title}>

            <div className="illustration-image">

              <img

                src={`/images/about/${interest.image}`}

                alt={interest.title}

                loading="lazy"

              />

            </div>



            <h4>{interest.title}</h4>

          </div>



        ))}

      </div>

    </div>

  </div>



</section>

{/* CONTACT */}
<section className="contact-section" id="contact">
  <div className="contact-left">
    <span className="section-label">CONTACT</span>

    <h2>
      Let's create
      <br />
      something.
    </h2>

    <p>
      Have a project, idea, or opportunity?
      <br />
      Let's talk.
    </p>
  </div>

  <div className="contact-right">
    <a
      href="mailto:officialamogh49@gmail.com"
      className="contact-email"
    >
      <span>OFFICIALAMOGH49@GMAIL.COM</span>
      <span aria-hidden="true">↗</span>
    </a>

    <div className="contact-socials">
      {/* LinkedIn */}
      <a
        href="https://www.linkedin.com/in/amoghputhanikar/"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="LinkedIn"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="currentColor"
          aria-hidden="true"
        >
          <path d="M19 3a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h14Zm-13.5 7v8h3v-8h-3Zm1.5-4.25a1.75 1.75 0 1 0 0 3.5 1.75 1.75 0 0 0 0-3.5ZM11 10v8h3v-4.2c0-1.1.2-2.2 1.6-2.2s1.4 1.3 1.4 2.3V18h3v-4.7c0-2.5-.5-4.4-3.5-4.4-1.4 0-2.3.7-2.7 1.4h-.1V10H11Z" />
        </svg>
      </a>

      {/* GitHub */}
      <a
        href="https://github.com/AmoghPuthanikar"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="GitHub"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="currentColor"
          aria-hidden="true"
        >
          <path d="M12 .5a12 12 0 0 0-3.79 23.39c.6.11.82-.26.82-.58v-2.23c-3.34.73-4.04-1.42-4.04-1.42-.55-1.39-1.33-1.76-1.33-1.76-1.09-.75.08-.74.08-.74 1.2.08 1.83 1.23 1.83 1.23 1.07 1.83 2.8 1.3 3.49.99.11-.77.42-1.3.76-1.6-2.67-.3-5.47-1.34-5.47-5.95 0-1.31.47-2.38 1.23-3.22-.12-.3-.53-1.52.12-3.17 0 0 1-.32 3.3 1.23a11.5 11.5 0 0 1 6 0c2.3-1.55 3.3-1.23 3.3-1.23.65 1.65.24 2.87.12 3.17.77.84 1.23 1.91 1.23 3.22 0 4.62-2.8 5.64-5.48 5.94.43.37.81 1.1.81 2.22v3.3c0 .32.22.7.83.58A12 12 0 0 0 12 .5Z" />
        </svg>
      </a>

      {/* Instagram */}
      <a
        href="https://www.instagram.com/amogh.design/"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Instagram"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          strokeWidth="2"
          strokeLinecap="round"
          strokeLinejoin="round"
          aria-hidden="true"
        >
          <rect x="2" y="2" width="20" height="20" rx="5" />
          <circle cx="12" cy="12" r="4" />
          <circle
            cx="18"
            cy="6"
            r="1"
            fill="currentColor"
            stroke="none"
          />
        </svg>
      </a>
    </div>
  </div>
</section>
    </main>

  );

}



export default App;