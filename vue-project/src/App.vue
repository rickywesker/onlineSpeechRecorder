<template>
  <div id="app">
    <TextRecorder :text="texts[current]" :index="current" :total="texts.length"/>
    <br>

    <button @click="next_text" v-if="current < texts.length-1">Next</button>
    <button @click="done" v-else>Done</button>
  </div>
</template>

<script>
import TextRecorder from "./components/TextRecorder";

export default {
  name: "App",
  components: {
    TextRecorder
  },
  data() {
    return {
      texts: [
        "History is the study of the past",
        "Events occurring before the invention of writing systems are considered prehistory",
        "History is an umbrella term that relates to past events as well as the memory, discovery, collection, organization, presentation, and interpretation of information about these events",
        "Historians place the past in context using historical sources such as written documents, oral accounts, ecological markers, and material objects including art and artifacts",
        "History also includes the academic discipline which uses narrative to describe, examine, question, and analyze a sequence of past events, investigate the patterns of cause and effect that are related to them",
        "Historians seek to understand and represent the past through narratives",
        "They often debate which narrative best explains an event, as well as the significance of different causes and effects",
        "Historians also debate the nature of history and its usefulness by discussing the study of the discipline as an end in itself and as a way of providing perspective on the problems of the present",
        "Stories common to a particular culture, but not supported by external sources (such as the tales surrounding King Arthur), are usually classified as cultural heritage or legends",
        "History differs from myth in that it is supported by evidence",
        "However, ancient influences have helped spawn variant interpretations of the nature of history which have evolved over the centuries and continue to change today",
        "The modern study of history is wide-ranging, and includes the study of specific regions and the study of certain topical or thematic elements of historical investigation",
        "History is often taught as part of primary and secondary education, and the academic study of history is a major discipline in university studies",
        "Herodotus, a 5th-century BC Greek historian is often considered (within the Western tradition) to be the father of history, or, by some, the father of lies",
        "Along with his contemporary Thucydides, he helped form the foundations for the modern study of human history",
        "Their works continue to be read today, and the gap between the culture-focused Herodotus and the military-focused Thucydides remains a point of contention or approach in modern historical writing",
        "In East Asia, a state chronicle, the Spring and Autumn Annals, was known to be compiled from as early as 722 BC although only 2nd-century BC texts have survived",
        "Historians write in the context of their own time, and with due regard to the current dominant ideas of how to interpret the past, and sometimes write to provide lessons for their own society",
        "In the words of Benedetto Croce, All history is contemporary history",
        "History is facilitated by the formation of a true discourse of past through the production of narrative and analysis of past events relating to the human race",
        "The modern discipline of history is dedicated to the institutional production of this discourse",
        "All events that are remembered and preserved in some authentic form constitute the historical record",
        "The task of historical discourse is to identify the sources which can most usefully contribute to the production of accurate accounts of past",
        "Therefore, the constitution of the historian's archive is a result of circumscribing a more general archive by invalidating the usage of certain texts and documents (by falsifying their claims to represent the true past",
        "Part of the historian's role is to skillfully and objectively utilize the vast amount of sources from the past, most often found in the archives",
        "The process of creating a narrative inevitably generates a silence as historians remember or emphasize different events of the past",
        "The study of history has sometimes been classified as part of the humanities and at other times as part of the social sciences",
        "It can also be seen as a bridge between those two broad areas, incorporating methodologies from both",
        "Some individual historians strongly support one or the other classification",
        "In the 20th century, French historian Fernand Braudel revolutionized the study of history, by using such outside disciplines as economics, anthropology, and geography in the study of global history",
        "Traditionally, historians have recorded events of the past, either in writing or by passing on an oral tradition, and have attempted to answer historical questions through the study of written documents and oral accounts",
        "From the beginning, historians have also used such sources as monuments, inscriptions, and pictures",
        "In general, the sources of historical knowledge can be separated into three categories: what is written, what is said, and what is physically preserved, and historians often consult all three",
        "But writing is the marker that separates history from what comes before",
        "Archaeology is especially helpful in unearthing buried sites and objects, which contribute to the study of history",
        "Archaeological finds rarely stand alone, with narrative sources complementing its discoveries",
        "Archaeology's methodologies and approaches are independent from the field of history",
        "Historical archaeology is a specific branch of archaeology which often contrasts its conclusions against those of contemporary textual sources",
        "For example, Mark Leone, the excavator and interpreter of historical Annapolis, Maryland, USA, has sought to understand the contradiction between textual documents idealizing liberty and the material record, demonstrating the possession of slaves and the inequalities of wealth made apparent by the study of the total historical environment",
        "There are varieties of ways in which history can be organized, including chronologically, culturally, territorially, and thematically",
        "These divisions are not mutually exclusive, and significant intersections are often present",
        "It is possible for historians to concern themselves with both the very specific and the very general, although the modern trend has been toward specialization",
        "The area called Big History resists this specialization, and searches for universal patterns or trends",
        "History has often been studied with some practical or theoretical aim, but also may be studied out of simple intellectual curiosity",
        "The historical method comprises the techniques and guidelines by which historians use primary sources and other evidence to research and then to write history",
        "Herodotus of Halicarnassus",
        "has generally been acclaimed as the father of history",
        "However, his contemporary Thucydides",
        "400 BC) is credited with having first approached history with a well-developed historical method in his work the History of the Peloponnesian War",
        "Thucydides, unlike Herodotus, regarded history as being the product of the choices and actions of human beings, and looked at cause and effect, rather than as the result of divine intervention (though Herodotus was not wholly committed to this idea himself)",
        "In his historical method, Thucydides emphasized chronology, a nominally neutral point of view, and that the human world was the result of the actions of human beings",
        "Greek historians also viewed history as cyclical, with events regularly recurring",
        "There were historical traditions and sophisticated use of historical method in ancient and medieval China",
        "The groundwork for professional historiography in East Asia was established by the Han dynasty court historian known as Sima Qian (145–90 BC), author of the Records of the Grand Historian (Shiji)",
        "For the quality of his written work, Sima Qian is posthumously known as the Father of Chinese historiography",
        "Chinese historians of subsequent dynastic periods in China used his Shiji as the official format for historical texts, as well as for biographical literature",
        "Saint Augustine was influential in Christian and Western thought at the beginning of the medieval period",
        "Through the Medieval and Renaissance periods, history was often studied through a sacred or religious perspective",
        "Around 1800, German philosopher and historian Georg Wilhelm Friedrich Hegel brought philosophy and a more secular approach in historical study",
        "In the preface to his book, the Muqaddimah (1377), the Arab historian and early sociologist, Ibn Khaldun, warned of seven mistakes that he thought that historians regularly committed",
        "In this criticism, he approached the past as strange and in need of interpretation",
        "The originality of Ibn Khaldun was to claim that the cultural difference of another age must govern the evaluation of relevant historical material, to distinguish the principles according to which it might be possible to attempt the evaluation, and lastly, to feel the need for experience, in addition to rational principles, in order to assess a culture of the past",
        "Ibn Khaldun often criticized idle superstition and uncritical acceptance of historical data",
        "As a result, he introduced a scientific method to the study of history, and he often referred to it as his new science",
        "His historical method also laid the groundwork for the observation of the role of state, communication, propaganda and systematic bias in history, and he is thus considered to be the father of historiography or the father of the philosophy of history"
      ],
      current: 0
    };
  },
  methods: {
    next_text() {
      this.current++;
    },
    done() {
      console.log("done");
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
