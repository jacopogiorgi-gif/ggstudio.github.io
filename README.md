import Image from "next/image";
import Link from "next/link";
import { ArrowDown, ArrowRight, ArrowUpRight, MoveUpRight } from "lucide-react";
import { desc, eq } from "drizzle-orm";
import { db } from "@/db";
import { articles } from "@/db/schema";
import { NewsCard } from "@/components/news-card";
import { ServiceIcon } from "@/components/service-icon";
import { services, site } from "@/lib/site";

export const dynamic = "force-dynamic";

export default async function HomePage() {
  const latestNews = await db.select().from(articles).where(eq(articles.published, true)).orderBy(desc(articles.publishedAt)).limit(3);

  return (
    <main>
      <section className="hero" aria-labelledby="hero-title">
        <div className="hero-copy">
          <div className="hero-copy-inner">
            <p className="eyebrow">GG STUDIO GIORGI <span className="eyebrow-dot">·</span> PRATO</p>
            <h1 id="hero-title">La tua impresa,<br /><em>una nuova</em><br />prospettiva.</h1>
            <p className="hero-description">Uno Studio di Dottori Commercialisti a Prato. Consulenza, visione e persone al tuo fianco per affrontare ogni sfida con maggiore consapevolezza.</p>
            <div className="hero-actions">
              <Link href="/studio" className="button button-dark">Scopri lo studio <ArrowUpRight size={18} strokeWidth={1.8} /></Link>
              <Link href="/contatti" className="text-link">Parla con noi <ArrowRight size={18} strokeWidth={1.7} /></Link>
            </div>
          </div>
          <div className="hero-bottom-note"><span>PROFESSIONISTI PER L’IMPRESA</span><a href="#approccio" aria-label="Scorri alla sezione il nostro approccio"><ArrowDown size={17} strokeWidth={1.5} /></a></div>
        </div>
        <div className="hero-visual">
          <Image src="/images/studio-archivio-2.jpg" alt="Area accoglienza dello Studio Giorgi a Prato" fill priority sizes="(max-width: 800px) 100vw, 52vw" className="hero-photo" />
          <div className="hero-photo-overlay" />
          <div className="hero-image-caption"><span className="caption-line" /><span>Un luogo dove le idee<br />trovano spazio.</span><MoveUpRight size={20} strokeWidth={1.5} /></div>
          <div className="hero-side-label">VIA GIUSEPPE VERDI 18 · PRATO</div>
        </div>
      </section>

      <section className="values-band" aria-label="Il nostro modo di lavorare">
        <div className="site-container values-inner">
          <div className="value-item"><span>01 / ASCOLTO</span><strong>Partiamo dalle persone.</strong></div>
          <div className="value-item"><span>02 / COMPETENZA</span><strong>Mettiamo a fuoco le soluzioni.</strong></div>
          <div className="value-item"><span>03 / VISIONE</span><strong>Guardiamo sempre avanti.</strong></div>
        </div>
      </section>

      <section className="intro-section section-space" id="approccio">
        <div className="site-container intro-grid">
          <div>
            <p className="eyebrow">IL NOSTRO APPROCCIO</p>
            <h2 className="section-title">Oltre i numeri,<br /><em>ci sono le persone.</em></h2>
          </div>
          <div className="intro-text">
            <p className="intro-lead">Ogni impresa è fatta di decisioni, opportunità e persone. Per questo crediamo in una consulenza che parte dall’ascolto e arriva lontano.</p>
            <p>GG Studio Giorgi nasce a Prato con un’idea semplice: affiancare imprese e professionisti con competenza, attenzione e uno sguardo capace di vedere l’insieme.</p>
            <Link href="/studio" className="underlined-link">Conosci la nostra storia <ArrowUpRight size={17} strokeWidth={1.7} /></Link>
          </div>
        </div>
      </section>

      <section className="services-section section-space" id="competenze">
        <div className="site-container">
          <div className="section-heading-row">
            <div><p className="eyebrow">COSA FACCIAMO</p><h2 className="section-title">Competenze diverse.<br /><em>Una sola direzione.</em></h2></div>
            <div className="section-heading-aside"><p>Un supporto completo, costruito intorno alle tue esigenze e a ogni fase del tuo percorso.</p><Link href="/competenze" className="underlined-link">Tutte le competenze <ArrowUpRight size={17} /></Link></div>
          </div>
          <div className="service-grid">
            {services.map((service) => <Link key={service.number} href={`/competenze#servizio-${service.number}`} className="service-card">
              <div className="service-card-top"><span className="service-icon"><ServiceIcon name={service.icon} /></span><span className="service-number">{service.number} / 06</span></div>
              <div><h3>{service.title}</h3><p>{service.short}</p></div>
              <span className="service-card-arrow" aria-hidden="true"><ArrowUpRight size={19} strokeWidth={1.6} /></span>
            </Link>)}
          </div>
        </div>
      </section>

      <section className="story-section section-space">
        <div className="site-container story-grid">
          <div className="story-visual">
            <div className="story-photo-primary"><Image src="/images/studio-07.jpg" alt="Opera d’arte esposta negli interni di GG Studio Giorgi" fill sizes="(max-width: 800px) 90vw, 42vw" /></div>
            <div className="story-photo-secondary"><Image src="/images/studio-04.jpg" alt="Libreria e dettagli negli uffici dello Studio" fill sizes="(max-width: 800px) 44vw, 20vw" /></div>
            <div className="story-photo-stamp">GG<span>STUDIO</span></div>
          </div>
          <div className="story-content">
            <p className="eyebrow">UNO STUDIO, TANTE PROSPETTIVE</p>
            <h2 className="section-title">Un luogo per<br /><em>pensare in grande.</em></h2>
            <p>Nel cuore di Prato, i nostri spazi raccontano chi siamo: professionali, accoglienti, aperti al dialogo. Perché le relazioni migliori cominciano sempre da un incontro.</p>
            <div className="story-points"><div><span>01</span><strong>Persone prima di tutto</strong></div><div><span>02</span><strong>Un dialogo che crea valore</strong></div><div><span>03</span><strong>Uno sguardo sul futuro</strong></div></div>
            <Link href="/studio" className="underlined-link">Entra nel nostro studio <ArrowUpRight size={17} /></Link>
          </div>
        </div>
      </section>

      <section className="news-section section-space" id="news">
        <div className="site-container">
          <div className="section-heading-row news-heading"><div><p className="eyebrow">NOVITÀ & APPROFONDIMENTI</p><h2 className="section-title">Idee da condividere.<br /><em>Notizie da conoscere.</em></h2></div><Link href="/news" className="underlined-link">Vai a tutte le news <ArrowUpRight size={17} /></Link></div>
          {latestNews.length > 0 ? (
            <div className="news-grid">{latestNews.map((article, index) => <NewsCard key={article.id} article={article} index={index} />)}</div>
          ) : (
            <div className="news-empty-feature">
              <div className="news-empty-photo"><Image src="/images/studio-archivio.jpg" alt="Insegna GG Studio Giorgi" fill sizes="(max-width: 800px) 100vw, 37vw" /></div>
              <div className="news-empty-copy"><span className="news-empty-kicker">IL NOSTRO SPAZIO NEWS <span>↗</span></span><h3>Uno spazio per restare <em>un passo avanti.</em></h3><p>Stiamo preparando notizie, spunti e approfondimenti per raccontarti quello che conta per la tua impresa.</p><Link href="/news" className="button button-light">Esplora la sezione <ArrowUpRight size={17} /></Link></div>
            </div>
          )}
        </div>
      </section>

      <section className="cta-section">
        <div className="site-container cta-inner"><div><p className="eyebrow eyebrow-light">IL PROSSIMO PASSO</p><h2>Le idee migliori iniziano<br />da una <em>conversazione.</em></h2><p>Raccontaci il tuo progetto. Troveremo insieme il modo giusto per farlo crescere.</p></div><Link href="/contatti" className="button button-white">Parliamone <ArrowUpRight size={18} /></Link></div>
        <div className="cta-watermark" aria-hidden="true">G</div>
      </section>
      <div className="quick-contact"><div className="site-container"><span>CI TROVI A PRATO</span><a href={site.mapsLink} target="_blank" rel="noopener noreferrer">Via Giuseppe Verdi n. 18 <ArrowUpRight size={15} /></a><span className="quick-contact-separator" /><a href={site.phoneHref}>{site.phone} <ArrowUpRight size={15} /></a></div></div>
    </main>
  );
}
