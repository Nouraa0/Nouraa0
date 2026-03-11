import React, { useState, useMemo } from 'react';
import { 
  Github, 
  Code2, 
  User, 
  Heart, 
  Briefcase, 
  BarChart3, 
  Copy, 
  Check, 
  Sparkles,
  Terminal,
  Coffee,
  Globe
} from 'lucide-react';
import ReactMarkdown from 'react-markdown';
import { clsx, type ClassValue } from 'clsx';
import { twMerge } from 'tailwind-merge';

/**
 * Utility for tailwind class merging
 */
function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}

export default function App() {
  const [name, setName] = useState('Your Name');
  const [username, setUsername] = useState('github_username');
  const [intro, setIntro] = useState('Hello there :)');
  const [aboutMe, setAboutMe] = useState('💻 CS Student at Suez Canal University (Faculty of Computers and Information).');
  const [skills, setSkills] = useState(['C++', 'Java', 'Python', 'HTML']);
  const [interests, setInterests] = useState('I am currently diving deep into the world of problem solving and algorithms. 🧠');
  const [projects, setProjects] = useState([
    { name: 'Awesome GUI Project', link: 'https://github.com/username/project1' },
    { name: 'Algorithm Visualizer', link: 'https://github.com/username/project2' }
  ]);
  const [theme, setTheme] = useState('dracula');
  const [copied, setCopied] = useState(false);

  const markdown = useMemo(() => {
    const skillsBadges = skills.map(skill => 
      `![${skill}](https://img.shields.io/badge/-${skill.replace('+', '%2B')}-333333?style=flat&logo=${skill.toLowerCase().includes('java') ? 'java' : skill.toLowerCase()})`
    ).join(' ');

    return `# Hi there! I'm ${name} 👋

${intro}

<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNHJ6Z3R6Z3R6Z3R6Z3R6Z3R6Z3R6Z3R6Z3R6Z3R6Z3R6Z3R6JmVwPXYxX2ludGVybmFsX2dpZl9ieV9pZCZjdD1n/L1R1tvI9svvvnGl2Z/giphy.gif" width="200" align="right" />

### 👩‍💻 About Me
${aboutMe}

👩‍💻 CS Student @ Suez Canal University  
🖥️ Into coding, GUIs.

### 🛠 Tech Stack
${skillsBadges}

### 🧠 Interests
${interests}

### 🚀 Projects
${projects.map(p => `- [${p.name}](${p.link})`).join('\n')}

### 📊 GitHub Stats
![GitHub Stats](https://github-readme-stats.vercel.app/api?username=${username}&show_icons=true&theme=${theme})
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=${username}&layout=compact&theme=${theme})
![GitHub Streak](https://github-readme-streak-stats.herokuapp.com/?user=${username}&theme=${theme})

---
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=auto&height=100&section=footer" />
</p>
`;
  }, [name, username, intro, aboutMe, skills, interests, projects, theme]);

  const handleCopy = () => {
    navigator.clipboard.writeText(markdown);
    setCopied(true);
    setTimeout(() => setCopied(false), 2000);
  };

  const addSkill = (e: React.KeyboardEvent<HTMLInputElement>) => {
    if (e.key === 'Enter') {
      const val = e.currentTarget.value.trim();
      if (val && !skills.includes(val)) {
        setSkills([...skills, val]);
        e.currentTarget.value = '';
      }
    }
  };

  const removeSkill = (skill: string) => {
    setSkills(skills.filter(s => s !== skill));
  };

  return (
    <div className="min-h-screen bg-[#FDFCF0] text-[#1A1A1A] font-sans selection:bg-[#FFD700]">
      {/* Header */}
      <header className="border-b border-[#1A1A1A]/10 bg-white/50 backdrop-blur-md sticky top-0 z-50">
        <div className="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="bg-[#1A1A1A] p-2 rounded-xl">
              <Github className="text-white w-6 h-6" />
            </div>
            <h1 className="text-xl font-bold tracking-tight">Profile README Generator</h1>
          </div>
          <button 
            onClick={handleCopy}
            className={cn(
              "flex items-center gap-2 px-5 py-2.5 rounded-full font-medium transition-all duration-300",
              copied 
                ? "bg-emerald-500 text-white shadow-lg shadow-emerald-200" 
                : "bg-[#1A1A1A] text-white hover:bg-[#333] shadow-lg shadow-black/10 active:scale-95"
            )}
          >
            {copied ? <Check size={18} /> : <Copy size={18} />}
            {copied ? 'Copied!' : 'Copy Markdown'}
          </button>
        </div>
      </header>

      <main className="max-w-7xl mx-auto p-6 grid grid-cols-1 lg:grid-cols-2 gap-8">
        {/* Editor Side */}
        <div className="space-y-8">
          <section className="bg-white rounded-3xl p-8 border border-[#1A1A1A]/5 shadow-sm">
            <div className="flex items-center gap-2 mb-6 text-[#1A1A1A]/40 uppercase text-[10px] font-bold tracking-widest">
              <User size={14} />
              <span>Basic Information</span>
            </div>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div className="space-y-2">
                <label className="text-xs font-semibold ml-1">Display Name</label>
                <input 
                  value={name}
                  onChange={e => setName(e.target.value)}
                  className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none"
                  placeholder="Your Name"
                />
              </div>
              <div className="space-y-2">
                <label className="text-xs font-semibold ml-1">GitHub Username</label>
                <input 
                  value={username}
                  onChange={e => setUsername(e.target.value)}
                  className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none"
                  placeholder="username"
                />
              </div>
            </div>
          </section>

          <section className="bg-white rounded-3xl p-8 border border-[#1A1A1A]/5 shadow-sm">
            <div className="flex items-center gap-2 mb-6 text-[#1A1A1A]/40 uppercase text-[10px] font-bold tracking-widest">
              <Sparkles size={14} />
              <span>Introduction & About</span>
            </div>
            <div className="space-y-6">
              <div className="space-y-2">
                <label className="text-xs font-semibold ml-1">Greeting / Intro</label>
                <input 
                  value={intro}
                  onChange={e => setIntro(e.target.value)}
                  className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none"
                />
              </div>
              <div className="space-y-2">
                <label className="text-xs font-semibold ml-1">About Me</label>
                <textarea 
                  value={aboutMe}
                  onChange={e => setAboutMe(e.target.value)}
                  rows={4}
                  className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none resize-none"
                />
              </div>
            </div>
          </section>

          <section className="bg-white rounded-3xl p-8 border border-[#1A1A1A]/5 shadow-sm">
            <div className="flex items-center gap-2 mb-6 text-[#1A1A1A]/40 uppercase text-[10px] font-bold tracking-widest">
              <Code2 size={14} />
              <span>Skills & Tech Stack</span>
            </div>
            <div className="space-y-4">
              <div className="flex flex-wrap gap-2">
                {skills.map(skill => (
                  <span 
                    key={skill}
                    onClick={() => removeSkill(skill)}
                    className="bg-[#1A1A1A] text-white text-[11px] font-medium px-3 py-1.5 rounded-full cursor-pointer hover:bg-red-500 transition-colors flex items-center gap-2 group"
                  >
                    {skill}
                    <span className="opacity-50 group-hover:opacity-100">×</span>
                  </span>
                ))}
              </div>
              <input 
                onKeyDown={addSkill}
                placeholder="Type a skill and press Enter..."
                className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none"
              />
            </div>
          </section>

          <section className="bg-white rounded-3xl p-8 border border-[#1A1A1A]/5 shadow-sm">
            <div className="flex items-center gap-2 mb-6 text-[#1A1A1A]/40 uppercase text-[10px] font-bold tracking-widest">
              <Heart size={14} />
              <span>Interests</span>
            </div>
            <textarea 
              value={interests}
              onChange={e => setInterests(e.target.value)}
              rows={2}
              className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none resize-none"
            />
          </section>

          <section className="bg-white rounded-3xl p-8 border border-[#1A1A1A]/5 shadow-sm">
            <div className="flex items-center gap-2 mb-6 text-[#1A1A1A]/40 uppercase text-[10px] font-bold tracking-widest">
              <BarChart3 size={14} />
              <span>Stats Theme</span>
            </div>
            <select 
              value={theme}
              onChange={e => setTheme(e.target.value)}
              className="w-full bg-[#F5F5F5] border-none rounded-2xl px-4 py-3 focus:ring-2 focus:ring-[#FFD700] transition-all outline-none appearance-none"
            >
              <option value="dracula">Dracula</option>
              <option value="radical">Radical</option>
              <option value="merko">Merko</option>
              <option value="gruvbox">Gruvbox</option>
              <option value="tokyonight">Tokyo Night</option>
              <option value="onedark">One Dark</option>
              <option value="cobalt">Cobalt</option>
              <option value="synthwave">Synthwave</option>
              <option value="highcontrast">High Contrast</option>
            </select>
          </section>
        </div>

        {/* Preview Side */}
        <div className="lg:sticky lg:top-24 h-fit">
          <div className="bg-white rounded-[32px] border border-[#1A1A1A]/5 shadow-xl overflow-hidden flex flex-col max-h-[calc(100vh-120px)]">
            <div className="px-8 py-4 border-b border-[#1A1A1A]/5 flex items-center justify-between bg-[#F9F9F9]">
              <div className="flex gap-1.5">
                <div className="w-2.5 h-2.5 rounded-full bg-[#FF5F57]" />
                <div className="w-2.5 h-2.5 rounded-full bg-[#FFBD2E]" />
                <div className="w-2.5 h-2.5 rounded-full bg-[#28C840]" />
              </div>
              <span className="text-[10px] font-bold text-[#1A1A1A]/30 uppercase tracking-widest">Live Preview</span>
              <div className="w-10" />
            </div>
            <div className="p-8 overflow-y-auto custom-scrollbar prose prose-slate max-w-none">
              <ReactMarkdown 
                components={{
                  img: ({node, ...props}) => <img {...props} referrerPolicy="no-referrer" className="rounded-lg" />,
                  h1: ({node, ...props}) => <h1 {...props} className="text-3xl font-bold mb-4" />,
                  h3: ({node, ...props}) => <h3 {...props} className="text-xl font-bold mt-8 mb-4 border-b pb-2" />,
                  p: ({node, ...props}) => <p {...props} className="text-gray-700 leading-relaxed mb-4" />,
                  ul: ({node, ...props}) => <ul {...props} className="list-disc pl-5 space-y-1 mb-4" />,
                }}
              >
                {markdown}
              </ReactMarkdown>
            </div>
          </div>
        </div>
      </main>

      {/* Footer */}
      <footer className="max-w-7xl mx-auto px-6 py-12 border-t border-[#1A1A1A]/5 mt-12">
        <div className="flex flex-col md:flex-row items-center justify-between gap-6 opacity-40 grayscale hover:grayscale-0 transition-all">
          <div className="flex items-center gap-2 text-sm font-medium">
            <Coffee size={16} />
            <span>Built for developers with love</span>
          </div>
          <div className="flex gap-8 text-[10px] font-bold uppercase tracking-widest">
            <a href="#" className="hover:text-[#FFD700]">Documentation</a>
            <a href="#" className="hover:text-[#FFD700]">Privacy</a>
            <a href="#" className="hover:text-[#FFD700]">Terms</a>
          </div>
        </div>
      </footer>

      <style>{`
        .custom-scrollbar::-webkit-scrollbar {
          width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
          background: transparent;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
          background: #E5E5E5;
          border-radius: 10px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
          background: #D1D1D1;
        }
      `}</style>
    </div>
  );
}
