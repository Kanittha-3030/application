<template>
  <v-card>
    <v-container fluid>
      <v-form ref="form" v-model="valid">
        <v-row>
          <v-col cols="10">

          </v-col>
          <v-col cols="2">
            <picture-input
              ref="pictureInput"
              width="300"
              height="300"
              margin="16"
              accept="image/jpeg, image/png"
              size="10"
              button-class="btn"
              :custom-strings="{
                upload: '<h1>Bummer!</h1>',
                drag: 'Drag a jpeg or png'
              }"
              @change="onChange"
            ></picture-input>
          </v-col>
        </v-row>
      <v-row align="center">
 
        <v-col cols="2" md="1.5">
          <v-select  v-model="datain.nt"
              :rules="rules.nt" :items="['นาย','นาง.','นางสาว']" label="คำนำหน้า(TH)" dense solo></v-select>
        </v-col>
        <v-col cols="5" md="3">
          <v-text-field  v-model="datain.namet"
              :rules="rules.namet" label="ชื่อ / (TH)" hint="ระบุเป็นภาษาไทย" dense outlined></v-text-field>
        </v-col>
        <v-col cols="5" md="3">
          <v-text-field  v-model="datain.surnamet"
              :rules="rules.surnamet" label="นามสกุล / (TH)" hint="ระบุเป็นภาษาไทย" dense outlined></v-text-field>
        </v-col>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nickt"
              :rules="rules.nt" label="ชื่อเล่น / (TH)" hint="ระบุเป็นภาษาไทย" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="2" md="1.5">
          <v-select  v-model="datain.ne"
              :rules="rules.ne" :items="['Mr.','Mrs.','Miss']"  label="คำนำหน้า(EN)" dense solo></v-select>
        </v-col>
        <v-col cols="5" md="3">
          <v-text-field  v-model="datain.namee"
              :rules="rules.namee" label="Name / (EN)" hint="ระบุเป็นภาษาอังกฤษ" dense outlined></v-text-field>
        </v-col>
        <v-col cols="5" md="3">
          <v-text-field  v-model="datain.surnamee"
              :rules="rules.surnamee" label="Surname / (EN)" hint="ระบุเป็นภาษาอังกฤษ" dense outlined></v-text-field>
        </v-col>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nicke"
              :rules="rules.nicke" label="Nickname / (EN)" hint="ระบุเป็นภาษาอังกฤษ" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          วันเกิด
          <br />Date of brith
        </v-subheader>
        <v-col cols="0" md="2">
          <v-text-field  v-model="datain.dofb"
              :rules="rules.dofb" label="DD/MM/YYYY" hint="DD/MM/YYYY" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          เพศ
          <br />Sex
        </v-subheader>
        <v-col cols="2" md="1">
          <v-select  v-model="datain.sex"
              :rules="rules.sex" :items="['Male','Female']"  label="Male/Female" dense solo></v-select>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field   v-model="datain.age"
              :rules="rules.age" label="อายุ/Age" hint="Age" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          เชื้อชาติ
          <br />Citizen
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.citizen"
              :rules="rules.citizen" label="เชื้อชาติ/Race" hint="Race" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สัญชาติ
          <br />Nationality
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nationality"
              :rules="rules.nationality" label="สัญชาติ/Nationality" hint="Nationality" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        
        <v-subheader>
          ศาสนา
          <br />Religion
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.religion"
              :rules="rules.religion" label="ศาสนา/Religion" hint="Religion" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ส่วนสูง
          <br />Height
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field  v-model="datain.height"
              :rules="rules.height" label="ระบุ.." hint="Height" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          น้ำหนัก
          <br />Weight
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field  v-model="datain.weight"
              :rules="rules.weight" label="ระบุ.." hint="Weight" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          กรุ๊ปเลือด
          <br />Blood Group
        </v-subheader>
        <v-col cols="2" md="1">
          <v-select  v-model="datain.blood"
              :rules="rules.blood" :items="['A','B','O','AB']"  label dense solo></v-select>
        </v-col>
      </v-row>
      <v-chip class="ma-2">ที่อยู่ปัจจุบัน/ Pressent</v-chip>
      <v-row>
        <v-subheader>
          บ้านเลขที่-หมู่ที่
          <br />House number
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field  v-model="datain.pr_add"
              :rules="rules.pr_add" label="บ้านเลขที่ / หมู่" hint="House number" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          หมู่บ้าน/อาคาร
          <br />Village/building
        </v-subheader>
        <v-col cols="3" md="3">
          <v-text-field  v-model="datain.pr_add"
              :rules="rules.pr_add" label="หมู่บ้าน/อาคาร" hint="Village/building" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ซอย
          <br />Alley
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_soi"
              :rules="rules.pr_soi" label="ซอย" hint="Alley" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ถนน
          <br />Street
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_street"
              :rules="rules.pr_street" label="ถนน" hint="Street" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          แขวง/ตำบล
          <br />District
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_district"
              :rules="rules.pr_district" label="แขวง/ตำบล" hint="District" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          เขต/อำเภอ
          <br />county
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_aumphur"
              :rules="rules.pr_aumphur" label="เขต/อำเภอ" hint="county" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          จังหวัด
          <br />county
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_proince"
              :rules="rules.pr_proince" label="จังหวัด" hint="county" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ประเทศ
          <br />county
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_proince"
              :rules="rules.pr_proince" label="ประเทศ" hint="county" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          รหัสไปรษณีย์
          <br />Postal code
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.pr_postaicode"
              :rules="rules.pr_postaicode" label="เขต/อำเภอ" hint="Postal code" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="3" md="3">
          <v-radio-group v-model="type" row>
            <v-radio label="บ้านตนเอง/Own house " dense outlined></v-radio>
            <v-radio label="ห้องเช่า/Rented room" dense outlined></v-radio>
          </v-radio-group>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          Telephone
          <br />โทรศัพท์บ้าน
        </v-subheader>
        <v-col  cols="2" md="2">
          <v-text-field   v-model="datain.nt"
              :rules="rules.nt" label="02 .." dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          Mobile
          <br />มือถือ
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.mobile"
              :rules="rules.mobile" label="+(66).." dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          Email
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.email"
              :rules="rules.email" label="example@gmail.com" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          Facebook
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.facebook"
              :rules="rules.facebook" label dense outlined></v-text-field>
        </v-col>
      </v-row>

      <v-chip class="ma-2">ที่อยู่ตามทะเบียนบ้าน/ Permanent address</v-chip>
      <v-row>
        <v-subheader>
          บ้านเลขที่
          <br />House number
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="บ้านเลขที่" hint="House number" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          หมู่บ้าน/อาคาร
          <br />Village/building
        </v-subheader>
        <v-col cols="3" md="3">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="หมู่บ้าน/อาคาร" hint="Village/building" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ซอย
          <br />Alley
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="ซอย" hint="Alley" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ถนน
          <br />Street
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="ถนน" hint="Street" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          แขวง/ตำบล
          <br />District
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="แขวง/ตำบล" hint="District" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          เขต/อำเภอ
          <br />county
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="เขต/อำเภอ" hint="county" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          จังหวัด
          <br />county
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="จังหวัด" hint="county" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          รหัสไปรษณีย์
          <br />Postal code
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field  v-model="datain.nt"
              :rules="rules.nt" label="เขต/อำเภอ" hint="Postal code" dense outlined></v-text-field>
        </v-col>
      </v-row>

      <v-row>
        <v-chip class="ma-2">การอุปสมบท/ Ordination</v-chip>
        <v-radio-group v-model="type" row>
          <v-radio label="ไม่เคย/ No" dense outlined></v-radio>
          <v-radio label="บวชเรียนแล้ว-ชื่อวัดและที่ตั้ง/ (Yes / where)" dense outlined></v-radio>
        </v-radio-group>

        <v-col cols="3" md="3">
          <v-text-field label="ระบุรายละเอียด" hint="Details" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-chip class="ma-2">สถานภาพการสมรส/ Marital status</v-chip>
        <v-radio-group v-model="type" row>
          <v-radio label="โสด/ Single" dense outlined></v-radio>
          <v-radio label="หย้า/ Divorced" dense outlined></v-radio>
          <v-radio label="หม้าย/ Widowed" dense outlined></v-radio>
          <v-radio label="สมรสจดทะเบียน/ Civil marriage" dense outlined></v-radio>
          <v-radio label="สมรสไม่จดทะเบียน/ Common-law marriage" dense outlined></v-radio>
        </v-radio-group>
      </v-row>
      <v-chip class="ma-2">ข้อมูลของคู่สมรสและบุตร / Family information</v-chip>
      <v-row>
        <v-col cols="2" md="1.5">
          <v-select :items="['นาย','นาง']" label="คำนำหน้า" dense solo></v-select>
        </v-col>
        <v-col cols="7" md="3">
          <v-text-field label="ชื่อ / (TH)" hint="ระบุเป็นภาษาไทย" dense outlined></v-text-field>
        </v-col>
        <v-col cols="5" md="3">
          <v-text-field label="นามสกุล / (TH)" hint="ระบุเป็นภาษาไทย" dense outlined></v-text-field>
        </v-col>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="Age" dense outlined></v-text-field>
        </v-col>
        <v-col cols="2" md="2">
          <v-text-field label="อำชีพ/ตำแหน่ง" hint="Occupation / Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          สถำนที่ทำงาน
          <br />Office address
        </v-subheader>
        <v-col cols="2" md="3">
          <v-text-field label="สถานที่ทำงาน" hint dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          โทรศัพท์
          <br />Telephone
        </v-subheader>
        <v-col cols="2" md="3">
          <v-text-field label="+66 .." hint dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-chip class="ma-2">จำนวนบุตร / Number of children</v-chip>
        <v-col cols="2" md="2">
          <v-select :items="['1','2','3','4','5']" label="จำนวนบุตร" dense solo></v-select>
        </v-col>
      </v-row>
      <v-chip
        class="ma-2"
      >ประวัติทางครอบครัว (ประวัติของบิดา / มารดา / พี่น้องทุกคน) / Family background</v-chip>
      <br />
      <v-chip class="ma-2">ควำมสัมพันธ์/ Relation</v-chip>
      <v-row>
        <v-subheader>
          บิดา
          <br />Father
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อาชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อาชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          มารดา
          <br />Father
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อำชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อาชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          พี่น้องลำดับที่1
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อำชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อำชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          พี่น้องลำดับที่2
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อาชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อาชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          พี่น้องลำดับที่3
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อาชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อาชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          พี่น้องลำดับที่4
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อาชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อาชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-subheader>
          พี่น้องลำดับที่5
          <br />
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ชื่อ/นามสกุล" hint="Name" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          อายุ
          <br />Age
        </v-subheader>
        <v-col cols="1" md="1">
          <v-text-field label="อายุ" hint="ระบุเป็นตัวเลข" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          สถานที่ทำงาน/โทรศัพท์
          <br />Company/Telephone
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="สถานที่ทำงาน/โทรศัพท์" hint="Company/Telephone" dense outlined></v-text-field>
        </v-col>
        <v-subheader>
          ตำแหน่ง/อาชีพ
          <br />Position
        </v-subheader>
        <v-col cols="2" md="2">
          <v-text-field label="ตำแหน่ง/อาชีพ" hint="Position" dense outlined></v-text-field>
        </v-col>
      </v-row>
      </v-form>
      <v-row>
        <v-btn color="primary" :disabled="!valid" @click="save()">Continue</v-btn>
      </v-row>
    </v-container>
  </v-card>
</template>
<script>
import PictureInput from "vue-picture-input";
export default {
  props: ["thisid"],
  components: {
    PictureInput
  },
  data() {
    return {
      data: null,
      valid: false,
      rules: {
        nt: [v => !!v || "Item is required"],
        namet: [
          v => !!v || "Name is required",
          v => (v && v.length >= 5) || "Name must be more than 5 characters",
          v => (v || "").indexOf(" ") < 0 || "No spaces are allowed"
        ],
        surnamet: [
          v => !!v || "Name is required",
          v => (v && v.length >= 5) || "Name must be more than 5 characters",
          v => (v || "").indexOf(" ") < 0 || "No spaces are allowed"
        ]
      },
      datain: {
        img: null,
        nt: "",
        namet: "",
        surnamet: "",
        nickt: "",
        ne: "",
        namee: "",
        surnamee: "",
        nicke: "",
        dofb: "",
        sex: "",
        age: "",
        citizen: "",
        nationality: "",
        religion: "",
        height: "",
        weight: "",
        blood: "",
        pr_add: "",
        pr_soi: "",
        pr_street: "",
        pr_district: "",
        pr_aumphur: "",
        pr_proince: "",
        pr_country: "",
        pr_postaicode: "",
        pr_map: "",

      }
    };
  },
  methods: {
    async init() {},
    onChange(image) {
      console.log("New picture selected!");
      if (image) {
        console.log("Picture loaded.");
        this.datain.img = image;
      } else {
        console.log("FileReader API not supported: use the <form>, Luke!");
      }
    },
    async save() {
      let urldata = process.env.VUE_APP_DATA;

      let res = await axios({
        method: "get",
        url: urldata + "/" + this.thisid
      });
      this.data = res.data;
      this.$parent.$parent.$parent.e6 = 2;
      let obj = Object.assign(this.data, this.datain);
      res = await axios({
        method: "put",
        url: urldata + "/" + this.thisid,
        data: obj
      });
    }
  },
  mounted() {
    this.init();
  }
};
</script>