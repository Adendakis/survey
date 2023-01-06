<template>
  <Survey :survey="survey" />
</template>

<script>
import 'survey-core/defaultV2.min.css';
import { StylesManager, Model } from 'survey-core';
import { Survey } from 'survey-vue-ui';

StylesManager.applyTheme("defaultV2");

const surveyJson = {
  
 "logoPosition": "right",
 "pages": [
  {
   "name": "page1",
   "elements": [
    {
     "type": "boolean",
     "name": "question6",
     "title": "Is the application still used to WRITE data?",
     "defaultValue": "false"
    },
    {
     "type": "boolean",
     "name": "question1",
     "title": "Is there a LEGAL REQUIREMENT to retain the data?",
     "defaultValue": "false"
    },
    {
     "type": "boolean",
     "name": "question7",
     "title": "Is there a WISH to retain/reuse the data for other purposes?",
     "defaultValue": "false"
    }
   ],
   "title": "Decomission/Archiving pattern"
  },
  {
   "name": "page2",
   "elements": [
    {
     "type": "radiogroup",
     "name": "question2",
     "title": "Which target language do you prefer",
     "defaultValue": "Item 3",
     "choices": [
      {
       "value": "Item 1",
       "text": "Cobol"
      },
      {
       "value": "Item 2",
       "text": "Java"
      },
      {
       "value": "Item 3",
       "text": "no preference"
      }
     ]
    },
    {
     "type": "radiogroup",
     "name": "question8",
     "title": "Will maintenance and development be in house or provided by third party?",
     "defaultValue": "Item 1",
     "choices": [
      {
       "value": "Item 1",
       "text": "Third Party"
      },
      {
       "value": "Item 2",
       "text": "own people"
      }
     ]
    },
    {
     "type": "boolean",
     "name": "question9",
     "title": "Do your people have skills in the new target language",
     "defaultValue": "true"
    }
   ],
   "title": "Migration/Refactoring pattern"
  },
  {
   "name": "page3",
   "elements": [
    {
     "type": "radiogroup",
     "name": "question3",
     "title": "Do you want to keep the code as is",
     "choices": [
      {
       "value": "Item 1",
       "text": "Yes"
      },
      {
       "value": "Item 2",
       "text": "No"
      }
     ]
    },
    {
     "type": "radiogroup",
     "name": "question4",
     "title": "Are your prgrammers capable of Java or will be trained",
     "choices": [
      {
       "value": "Item 1",
       "text": "Yes"
      },
      {
       "value": "Item 2",
       "text": "No"
      }
     ]
    },
    {
     "type": "boolean",
     "name": "question5"
    }
   ],
   "title": "NonDecommision"
  }
 ],
 "triggers": [
  {
   "type": "complete",
   "expression": "{question1} = true and {question7} = true"
  }
 ]
};
 

export default {
  name: 'MyFirstSurvey',
  components: {
    Survey
  },
  data() {
    const survey = new Model(surveyJson);
    survey.onComplete.add(this.alertResults);

    return {
      survey
    }
  },
  methods: {
    alertResults (sender) {
      const results = JSON.stringify(sender.data);
      alert(results);
    }
  },
}
</script>