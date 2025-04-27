# One-tab-polygot
import React, { useState } from 'react';


const translations = {
  // English to Spanish
  "en-es": {
    "hello": "hola",
    "goodbye": "adiós",
    "thank you": "gracias",
    "please": "por favor",
    "yes": "sí",
    "no": "no",
    "good morning": "buenos días",
    "good afternoon": "buenas tardes",
    "good evening": "buenas noches",
    "how are you": "¿cómo estás?",
    "my name is": "me llamo",
    "what is your name": "¿cómo te llamas?",
    "i don't understand": "no entiendo",
    "excuse me": "disculpe",
    "help": "ayuda",
    "water": "agua",
    "food": "comida",
    "where is": "dónde está",
    "how much": "cuánto cuesta",
    "today": "hoy",
    "tomorrow": "mañana",
    "yesterday": "ayer"
  },
  // English to French
  "en-fr": {
    "hello": "bonjour",
    "goodbye": "au revoir",
    "thank you": "merci",
    "please": "s'il vous plaît",
    "yes": "oui",
    "no": "non",
    "good morning": "bonjour",
    "good afternoon": "bon après-midi",
    "good evening": "bonsoir",
    "how are you": "comment allez-vous?",
    "my name is": "je m'appelle",
    "what is your name": "comment vous appelez-vous?",
    "i don't understand": "je ne comprends pas",
    "excuse me": "excusez-moi",
    "help": "aide",
    "water": "eau",
    "food": "nourriture",
    "where is": "où est",
    "how much": "combien ça coûte",
    "today": "aujourd'hui",
    "tomorrow": "demain",
    "yesterday": "hier"
  },
  // English to German
  "en-de": {
    "hello": "hallo",
    "goodbye": "auf wiedersehen",
    "thank you": "danke",
    "please": "bitte",
    "yes": "ja",
    "no": "nein",
    "good morning": "guten morgen",
    "good afternoon": "guten tag",
    "good evening": "guten abend",
    "how are you": "wie geht's?",
    "my name is": "ich heiße",
    "what is your name": "wie heißt du?",
    "i don't understand": "ich verstehe nicht",
    "excuse me": "entschuldigung",
    "help": "hilfe",
    "water": "wasser",
    "food": "essen",
    "where is": "wo ist",
    "how much": "wie viel kostet",
    "today": "heute",
    "tomorrow": "morgen",
    "yesterday": "gestern"
  },
  // English to Italian
  "en-it": {
    "hello": "ciao",
    "goodbye": "arrivederci",
    "thank you": "grazie",
    "please": "per favore",
    "yes": "sì",
    "no": "no",
    "good morning": "buongiorno",
    "good afternoon": "buon pomeriggio",
    "good evening": "buonasera",
    "how are you": "come stai?",
    "my name is": "mi chiamo",
    "what is your name": "come ti chiami?",
    "i don't understand": "non capisco",
    "excuse me": "scusa",
    "help": "aiuto",
    "water": "acqua",
    "food": "cibo",
    "where is": "dov'è",
    "how much": "quanto costa",
    "today": "oggi",
    "tomorrow": "domani",
    "yesterday": "ieri"
  },
  // English to Japanese (romanized)
  "en-ja": {
    "hello": "konnichiwa",
    "goodbye": "sayonara",
    "thank you": "arigatou",
    "please": "onegaishimasu",
    "yes": "hai",
    "no": "iie",
    "good morning": "ohayou gozaimasu",
    "good afternoon": "konnichiwa",
    "good evening": "konbanwa",
    "how are you": "ogenki desu ka?",
    "my name is": "watashi no namae wa",
    "what is your name": "onamae wa nan desu ka?",
    "i don't understand": "wakarimasen",
    "excuse me": "sumimasen",
    "help": "tasukete",
    "water": "mizu",
    "food": "tabemono",
    "where is": "doko ni",
    "how much": "ikura desu ka",
    "today": "kyou",
    "tomorrow": "ashita",
    "yesterday": "kinou"
  },
  // English to Chinese (romanized)
  "en-zh": {
    "hello": "ni hao",
    "goodbye": "zai jian",
    "thank you": "xie xie",
    "please": "qing",
    "yes": "shi",
    "no": "bu shi",
    "good morning": "zao shang hao",
    "good afternoon": "xia wu hao",
    "good evening": "wan shang hao",
    "how are you": "ni hao ma?",
    "my name is": "wo jiao",
    "what is your name": "ni jiao shen me ming zi?",
    "i don't understand": "wo bu dong",
    "excuse me": "dui bu qi",
    "help": "bang zhu",
    "water": "shui",
    "food": "shi wu",
    "where is": "zai na li",
    "how much": "duo shao qian",
    "today": "jin tian",
    "tomorrow": "ming tian",
    "yesterday": "zuo tian"
  }
};

// List of supported languages
const supportedLanguages = [
  { code: "es", name: "Spanish" },
  { code: "fr", name: "French" },
  { code: "de", name: "German" },
  { code: "it", name: "Italian" },
  { code: "ja", name: "Japanese" },
  { code: "zh", name: "Chinese" }
];

export default function LanguageConverter() {
  const [inputText, setInputText] = useState("");
  const [outputText, setOutputText] = useState("");
  const [selectedLanguage, setSelectedLanguage] = useState("es");
  const [sourceLanguage, setSourceLanguage] = useState("en");

  const translateText = () => {
    if (!inputText) {
      setOutputText("");
      return;
    }

    const langPair = `${sourceLanguage}-${selectedLanguage}`;
    const dict = translations[langPair];
    
    if (!dict) {
      setOutputText("Translation not available for this language pair");
      return;
    }

    // Simple word-by-word translation
    const words = inputText.toLowerCase().split(/\s+/);
    const translatedWords = words.map(word => {
      // Check for exact match
      if (dict[word]) {
        return dict[word];
      }
      
      // Check for phrases
      for (const [phrase, translation] of Object.entries(dict)) {
        if (phrase.includes(word)) {
          return translation;
        }
      }
      
      // If no translation found, return the original word
      return word;
    });

    setOutputText(translatedWords.join(" "));
  };

  return (
    <div className="flex flex-col p-4 max-w-2xl mx-auto bg-gray-50 rounded-lg shadow-md">
      <h1 className="text-2xl font-bold text-center mb-6">Language Translator</h1>
      
      <div className="mb-4">
        <label className="block text-gray-700 mb-2">From:</label>
        <select 
          className="w-full p-2 border rounded"
          value={sourceLanguage}
          onChange={(e) => setSourceLanguage(e.target.value)}
        >
          <option value="en">English</option>
          {supportedLanguages.map(lang => (
            <option key={lang.code} value={lang.code}>{lang.name}</option>
          ))}
        </select>
      </div>
      
      <div className="mb-4">
        <label className="block text-gray-700 mb-2">To:</label>
        <select 
          className="w-full p-2 border rounded"
          value={selectedLanguage}
          onChange={(e) => setSelectedLanguage(e.target.value)}
        >
          {supportedLanguages.map(lang => (
            <option key={lang.code} value={lang.code}>{lang.name}</option>
          ))}
        </select>
      </div>
      
      <div className="mb-4">
        <label className="block text-gray-700 mb-2">Enter text:</label>
        <textarea 
          className="w-full p-2 border rounded h-32"
          value={inputText}
          onChange={(e) => setInputText(e.target.value)}
          placeholder="Type text to translate..."
        />
      </div>
      
      <button 
        className="bg-blue-500 text-white py-2 px-4 rounded hover:bg-blue-600 mb-4"
        onClick={translateText}
      >
        Translate
      </button>
      
      <div className="mb-4">
        <label className="block text-gray-700 mb-2">Translation:</label>
        <div className="w-full p-2 border rounded min-h-32 bg-white">
          {outputText || "Translation will appear here"}
        </div>
      </div>
      
      <div className="text-sm text-gray-500 mt-4">
        <p>Note: This is a basic translator with a limited dictionary. It translates common words and phrases only.</p>
      </div>
    </div>
  );
}
