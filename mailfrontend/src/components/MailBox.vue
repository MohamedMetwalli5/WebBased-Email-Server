<template>
  <div class="MailBox">
    <!-- <compose /> -->
    <div class="page">
      <div class="optionsColumn">
        <button id="sendOption" onclick="window.location.href='/SendEmail';">
          Send Email ✏️
        </button>
        <div pageOptionDiv>
          <button
            id="inboxBtn"
            @click="
              //SetButtonColorInbox(),
              (pageOption = 'Inbox Mail ✉️'),
                ChangePage(),
                (pageNumber = 1),
                (document.getElementById('pageNumberOneOption').value = true),
                (document.getElementById('pageNumberOneOption').checked = true),
                console.log('pageNumber'),
                (folderName = 'Inbox')
            "
            class="pageOption"
          >
            Inbox 📫
          </button>
        </div>
        <div pageOptionDiv>
          <button
            id="trashBtn"
            @click="
              // SetButtonColorTrash(),
              (pageOption = 'Trash Box🗑️'),
                (pageNumber = 1),
                ChangePage(),
                (document.getElementById('pageNumberOneOption').value = true),
                (document.getElementById('pageNumberOneOption').checked = true),
                console.log('pageNumber'),
                (folderName = 'Trash')
            "
            class="pageOption"
          >
            Trash 🗑️
          </button>
        </div>
        <div pageOptionDiv>
          <button
            class="pageOption"
            @click="
              (pageOption = 'Drafts 📋'),
                ChangePage(),
                (pageNumber = 1),
                (folderName = 'Draft')
            "
          >
            Drafts 📋
          </button>
        </div>
        <div pageOptionDiv>
          <button
            class="pageOption"
            @click="
              (pageOption = 'Sent 📧'),
                ChangePage(),
                (pageNumber = 1),
                (folderName = 'Sent')
            "
          >
            Sent 📧
          </button>
        </div>
        <div pageOptionDiv>
          <button
            class="pageOption"
            onclick="window.location.href='/Contacts';"
          >
            Contacts 📔
          </button>
        </div>
        <div pageOptionDiv>
          <button class="pageOption" onclick="window.location.href='/Folders';">
            Folders 📁
          </button>
        </div>
      </div>
      <div class="displayColumn">
        <div>
          <h1 id="theInboxTitle">{{ pageOption }}</h1>
          <ul class="emailsOperationDiv">
            <li class="emailsOperationButton">
              Filter
              <div class="subMenu-2">
                <ul>
                  <button class="menuElement" @click="Filter()">Subject</button>
                  <input type="text" id="filterSubjectText" />

                  <br />
                  <button class="menuElement" @click="Filter()">Sender</button>
                  <input type="text" id="filterSenderText" />
                </ul>
              </div>
            </li>
            <li class="emailsOperationButton">
              Sort
              <div class="subMenu-1">
                <ul>
                  <button class="menuElement" @click="sortText = 'Priority'">
                    Priority
                  </button>
                  <button class="menuElement" @click="sortText = 'Date'">
                    Date
                  </button>
                  <button class="menuElement" @click="sortText = 'Sender'">
                    Sender
                  </button>
                  <button class="menuElement" @click="sortText = 'Subject'">
                    Subject
                  </button>
                </ul>
              </div>
            </li>
            <button
              class="emailsOperationButton"
              @click="Seacrh(this.document.text.value)"
            >
              Search<input type="text" id="searchText" value="" />
            </button>
            <button class="menuElement" @click="open()"> open </button>
          </ul>
          <div id="pageNumberOptionsDiv">
            <h2>1 2 3 4</h2>
            <input
              type="radio"
              id="pageNumberOneOption"
              name="radioButtonPageNumberOption"
              value="false"
              checked="false"
              @click="(pageNumber = 1), ChangePage()"
            />

            <input
              type="radio"
              id="pageNumberTwoOption"
              name="radioButtonPageNumberOption"
              value="false"
              @click="(pageNumber = 2), ChangePage()"
            />
            <input
              type="radio"
              id="pageNumbeThreerOption"
              name="radioButtonPageNumberOption"
              value="false"
              @click="(pageNumber = 3), ChangePage()"
            />
            <input
              type="radio"
              id="pageNumberFourOption"
              name="radioButtonPageNumberOption"
              value="false"
              @click="(pageNumber = 4), ChangePage()"
            />
          </div>
          <br />
        </div>
        <table class="table">
          <tr id="titleRow">
            <td class="checkBoxClass">&nbsp;</td>
            <td @click="Sort('Sender')">Sender</td>
            <td @click="Sort('Subject')">Subject</td>
            <td @click="Sort('Priority')">Priority</td>
            <td @click="Sort('Date')">Date</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input
                type="radio"
                name="EmailsOption"
                value="false"
                @click="namePointer = 1"
              />
            </td>
            <td class="rOption">
              {{ sender[0] }}
            </td>
            <td class="rOption">{{ subject[0] }}</td>
            <td class="rOption">{{ priority[0] }}</td>
            <td class="rOption">{{ date[0] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer = 2" />
            </td>
            <td class="rOption">{{ sender[1] }}</td>
            <td class="rOption">{{ subject[1] }}</td>
            <td class="rOption">{{ priority[1] }}</td>
            <td class="rOption">{{ date[1] }}</td>
          </tr>
          <tr class="row">
            <td><input type="radio" name="EmailsOption" value="false" @click="namePointer = 2" /></td>
            <td class="rOption">{{ sender[2] }}</td>
            <td class="rOption">{{ subject[2] }}</td>
            <td class="rOption">{{ priority[2] }}</td>
            <td class="rOption">{{ date[2] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer = 4"/>
            </td>
            <td class="rOption">{{ sender[3] }}</td>
            <td class="rOption">{{ subject[3] }}</td>
            <td class="rOption">{{ priority[3] }}</td>
            <td class="rOption">{{ date[3] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="this.namePointer = 5"/>
            </td>
            <td class="rOption">{{ sender[4] }}</td>
            <td class="rOption">{{ subject[4] }}</td>
            <td class="rOption">{{ priority[4] }}</td>
            <td class="rOption">{{ date[4] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer = 6"/>
            </td>
            <td class="rOption">{{ sender[5] }}</td>
            <td class="rOption">{{ subject[5] }}</td>
            <td class="rOption">{{ priority[5] }}</td>
            <td class="rOption">{{ date[5] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer = 7"/>
            </td>

            <td class="rOption">{{ sender[6] }}</td>
            <td class="rOption">{{ subject[6] }}</td>
            <td class="rOption">{{ priority[6] }}</td>
            <td class="rOption">{{ date[6] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer = 8"/>
            </td>
            <td class="rOption">{{ sender[7] }}</td>
            <td class="rOption">{{ subject[7] }}</td>
            <td class="rOption">{{ priority[7] }}</td>
            <td class="rOption">{{ date[7] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer =9"/>
            </td>
            <td class="rOption">{{ sender[8] }}</td>
            <td class="rOption">{{ subject[8] }}</td>
            <td class="rOption">{{ priority[8] }}</td>
            <td class="rOption">{{ date[8] }}</td>
          </tr>
          <tr class="row">
            <td class="rOption">
              <input type="radio" name="EmailsOption" value="false" @click="namePointer = 10"/>
            </td>
            <td class="rOption">{{ sender[9] }}</td>
            <td class="rOption">{{ subject[9] }}</td>
            <td class="rOption">{{ priority[9] }}</td>
            <td class="rOption">{{ date[9] }}</td>
          </tr>
        </table>
      </div>
    </div>
    <!-- -->
  </div>
</template>

<script>
import "../filter.js";
//import compose from "../components/compose";
const axios = require("axios").default;
export default {
  name: "MailBox",

  data: function () {
    return {
      pageOption: "Inbox Mail ✉️", //the folder name
      contacts: [null].fill(null),
      sender: [].fill(null),
      subject: [].fill(null),
      priority: [].fill(null),
      date: [].fill(null),
      checkMark: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      senderFilterText: "null",
      subjectFilterText: "null",
      sortText: "null",
      searchText: "null",
      pageNumber: 1,
      folderName: "inbox",
      namePointer:0
    };
  },

  methods: {
    //loading whenevrer the user login immediately
    displayCompose: function () {
      document.getElementById("sendOption").style.display = "block";
    },
    ChangePage: function () {
      //to load the emails
      axios
        .get("http://localhost:8080/loadEmails", {
          params: { page: this.pageNumber, folderName: this.folderName },
        })
        .then((response) => {
          console.log(response.data);
          for (var i = 0; i < response.data.length; i++) {
            this.$set(this.sender, i, response.data[i].sender);
            this.$set(this.subject, i, response.data[i].subject);
            this.$set(this.priority, i, response.data[i].priority);
            this.$set(this.date, i, response.data[i].date);
          }

          console.log("pageNumber is " + this.pageNumber);
        });
    },
    Filter: function () {
      this.senderFilterText = document.getElementById("filterSenderText").value;
      this.subjectFilterText = document.getElementById(
        "filterSubjectText"
      ).value;
      console.log(this.senderFilterText + "  " + this.subjectFilterText);
      axios
        .get("http://localhost:8080/filterEmails", {
          params: {
            filterNameSender: this.senderFilterText,
            filterNameSubject: this.subjectFilterText,
          },
        })
        .then((response) => {
          console.log(response.data);
          for (var i = 0; i < response.data.length; i++) {
            console.log(i);
            this.$set(this.sender, i, response.data[i].sender);
            this.$set(this.subject, i, response.data[i].subject);
            this.$set(this.priority, i, response.data[i].priority);
            this.$set(this.date, i, response.data[i].date);
          }
          console.log("pageNumber is " + this.pageNumber);
        });
    },

    Sort: function (sortText) {
      axios
        .get("http://localhost:8080/sorter", {
          params: {
            sortKey: this.sortText,
          },
        })
        .then((response) => {
          console.log(sortText);
          console.log(response.data);
          for (var i = 0; i < response.data.length; i++) {
            this.$set(this.sender, i, response.data[i].sender);
            this.$set(this.subject, i, response.data[i].subject);
            this.$set(this.priority, i, response.data[i].priority);
            this.$set(this.date, i, response.data[i].date);
          }

          console.log("pageNumber is " + this.pageNumber);
        });
    },
    Search: function (searchText) {
      this.searchKey = document.getElementById("searchText").value;
      console.log(searchText);
      axios
        .get("http://localhost:8080/searcher", {
          params: {
            searchKey: this.searchText,
          },
        })
        .then((response) => {
          console.log(response.data);
          for (var i = 0; i < response.data.length; i++) {
            this.$set(this.sender, i, response.data[i].sender);
            this.$set(this.subject, i, response.data[i].subject);
            this.$set(this.priority, i, response.data[i].priority);
            this.$set(this.date, i, response.data[i].date);
          }

          console.log("pageNumber is " + this.pageNumber);
        });
    },
    open: function (){
      //the name of the email need to be opened
      //console.log(this.namePointer);
      //this.sender[this.namePointer-1]
      //tell the backend which file need to be opened
      if (!(typeof this.date[this.namePointer-1] === 'undefined')&&!(typeof this.sender[this.namePointer-1] === 'undefined')) {
        console.log(this.date[this.namePointer-1]);
      console.log(this.sender[this.namePointer-1]);
      var emailName=this.date[this.namePointer-1]+this.sender[this.namePointer-1];
      console.log(emailName);
      var v = new FormData();
      v.append("currentEmail", emailName);
      axios
          .post("http://localhost:8080/setCurrentEmail", v)
          .then((response) => {
            console.log(response.data);
          })
          .catch((e) => {
            console.log(e);
          });
      //go to show email interface in the frontend
      window.location.href = "/email";
      }
    }
  },

  /* computed: {
    showSubject: function () {
      return this.sender[0].userId;
    },
  },
  */
};
</script>
<style  scoped>
.ButtonsGroup {
  background-image: linear-gradient(-45deg, rgb(59, 203, 228), magenta);
  border-radius: 20px;
  margin-top: 1px;
  width: 100%;
  height: 5%;
}

.b {
  margin: auto;
  margin-top: 5px;
  margin-bottom: 5px;
  font-size: 20px;
  font-style: oblique;
  width: 10%;
  height: 80%;
  background-color: linear-gradient(
    -100deg,
    rgb(153, 35, 168),
    rgb(213, 233, 31)
  );
  background: linear-gradient(-100deg, rgb(72, 212, 16), rgb(215, 236, 21));
  border-radius: 20px;
}

#theInboxTitle {
  text-align: left;
  line-height: 70px;
  font-size: 50px;
  color: rgb(36, 47, 196);
  margin: auto;
  margin-top: 0px;
  padding-left: 10px;
  height: 90px;
  border: solid;
  border-radius: 20px;
  background: linear-gradient(-45deg, rgb(238, 189, 30), rgb(255, 238, 0));
}

.optionsColumn {
  float: left;
  width: 12%;
  padding: 10px;
  height: 100%px;
  border: solid;
  border-radius: 15px;
  border-color: red;
  margin-top: 10px;
}
.displayColumn {
  float: left;
  margin-left: 2%;
  width: 70%;
  padding: 10px;
  height: 1000px;
}

#sendOption {
  height: 120px;
  margin-top: 150px;
  border-radius: 20px;
  border: solid;
  color: green;
  background: white;
  font-size: 40px;
  font-weight: bold;
  margin-bottom: 30px;
  margin-top: 20px;
}

#sendOption:hover {
  background: rgb(108, 225, 240);
}

.pageOption {
  width: 150px;
  height: 70px;
  border-radius: 20px;
  border: solid;
  color: green;
  background: white;
  font-size: 30px;
  font-weight: bold;
  margin: auto;
  margin-bottom: 30px;
}
.pageOption:hover {
  background: rgb(129, 241, 148);
}

.pageOptionDiv {
  background-image: black;
  color: aqua;
}

.table {
  margin: auto;
  width: 100%;
  height: 100%;
  border-radius: 20px;
  border: solid;
  border-color: white;
}

#titleRow {
  border-radius: 20px;
  width: 100%;
  height: 10%;
  font-size: 35px;
  font-weight: bolder;
  color: rgb(243, 45, 184);
  margin: auto;
  margin-bottom: 10px;
  border-bottom: solid;
  border-color: cyan;
}

.row {
  border: solid;
  border-radius: 20px;
  border-bottom: black;
  color: black;
  margin: auto;
  margin-bottom: 5px;
  font-size: 20px;
}

.row:hover {
  background: rgb(108, 240, 174);
}
.rOption {
  /* used to make the underline between emails */
  border-top: solid;
  border-bottom: rgb(0, 0, 0);
}

#pageNumberOptionsDiv {
  line-height: 5px;
  padding-bottom: 4px;
  margin-top: 140px;
  border-radius: 25px;
  margin-left: 40%;
  width: 100px;
  color: rgb(29, 201, 6);
  border: solid;
}

.emailsOperationDiv {
  display: inline-flex;
  float: left;
  margin-top: 20px;
  width: 100%px;
  color: rgb(226, 40, 211);
  border: solid;
  border-radius: 40px;
  background: blueviolet;
  height: 10%px;
}
.emailsOperationButton {
  margin-right: 150px;
  line-height: 30px;
  float: left;
  width: 120px;
  color: rgb(255, 255, 255);
  border: solid;
  border-color: brown;
  border-radius: 20px;
  background: rgb(235, 74, 74);
  height: 30px;
}

.emailsOperationButton:hover {
  background: rgb(50, 230, 74);
}

.subMenu-1 {
  display: none;
  border-bottom: solid;
  border-color: brown;
  border-radius: 20px;
  background: rgb(235, 74, 74);
}

.menuElement {
  float: left;
  padding-left: 5px;
  margin-left: 10px;
  margin-right: 20px;
  background: cyan;
  color: black;
  border: solid;
  border-radius: 20px;
  height: 30px;
}

.menuElement:hover {
  background: rgb(9, 194, 194);
}

.emailsOperationButton:hover .subMenu-1 {
  text-align: left;
  margin-top: 0px;
  display: block;
  position: absolute;
  border-radius: 20px;
  border: solid;
  border-color: brown;
  background: rgb(241, 103, 103);
  height: 30px;
}

#searchText {
  margin-top: 10%;
  height: 30px;
  font-size: 20px;
  background: whitesmoke;
}

#filterSubjectText {
  background: whitesmoke;
  border-radius: 10px;
}

#filterSenderText {
  background: whitesmoke;
  border-radius: 10px;
}

.subMenu-2 {
  display: none;
  float: left;
  border: solid;
  border-radius: 20px;
  border-color: brown;
  background: rgb(241, 103, 103);
  width: 220px;
}

.emailsOperationButton:hover .subMenu-2 {
  text-align: left;
  margin-top: 0px;
  display: block;
  position: absolute;
  float: left;
  border: solid;
  border-radius: 20px;
  border-color: brown;
  background: rgb(241, 103, 103);
  width: 220px;
}
</style>