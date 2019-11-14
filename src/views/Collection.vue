<template>
  <v-layout class="collection" flex-wrap>
    <v-row>
      <v-col
        v-for="image in this.images"
        :key="image.index"
        class="d-flex child-flex"
        cols="12"
        sm="6"
        md="3"
      >
        <v-card flat tile class="d-flex" @click="openModal(image)">
          <v-img
            :src="image.src"
            aspect-ratio="1"
            class="grey lighten-1"
          >
            <template v-slot:placeholder>
              <v-row
                class="fill-height"
                align="center"
                justify="center"
              >
                <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-card>
      </v-col>
    </v-row>
    <v-dialog v-model="dialog.status" max-width="500px" class="dialog" overlay-opacity="1" :overlay-color="this.selected.color">
      <v-card>
        <v-img
          height="350px"
          aspect-ratio="1"
          :src="dialog.info.src"
        />
        <v-card-title class="dialog__title">
          <p class="dialog__name">{{ dialog.info.name }}</p>
        </v-card-title>
        <v-card-text>
          <p class="dialog__company">
            <span>
              <v-avatar color="white" size="25">
                <v-img
                  :src="this.selected.src"
                />
              </v-avatar>
            </span>
            <span class="dialog__company__name">{{ dialog.info.sub || '' }}</span>
          </p>
          <p>{{ dialog.info.address }}</p>
          <p>
            <span
              class="dialog__location"
              @click="openGoogleMaps(dialog.info.lat, dialog.info.lon)"
            >
              {{ `${dialog.info.lat}, ${dialog.info.lon}`}}
            </span>
          </p>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn :color="`${this.selected.color} darken-2`" text @click="closeModal">Close</v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
export default {
  name: 'Collection',
  data() {
    return {
      dialog: {
        status: false,
        info: {
          name: '',
          address: '',
          sub: '',
          lat: 0,
          lon: 0
        }
      },
      images: [
        // -------- GOOGLE DATA CENTERS --------
        {
          name: 'Google Data Center',
          address: '4200 Columbia Rd, The Dalles, OR 97058',
          sub: 'Google',
          src: require('@/assets/google/1.jpg'),
          lat: 45.632511,
          lon: -121.202267
        },
        {
          name: 'Quilicura Google Data Center',
          address: '2130,, El Molino, Quilicura, Región Metropolitana, Chile',
          sub: 'Google',
          src: require('@/assets/google/2.jpg'),
          lat: -33.358472,
          lon: -70.697333
        },
        {
          name: 'Belgium Google Data Center',
          address: 'BE-GBL-DAT2A, 7331 Saint-Ghislain, Belgium',
          sub: 'Google',
          src: require('@/assets/google/3.jpg'),
          lat: 50.469333,
          lon: 3.865472
        },
        {
          name: 'Tuike Finland Oy',
          address: 'Ensontie 1, 49420 Hamina, Finland',
          sub: 'Google',
          src: require('@/assets/google/4.jpg'),
          lat: 60.536578,
          lon: 27.117003
        },
        {
          name: 'Dublin Google Data Center',
          address: 'Nangor, Co. Dublin, Ireland',
          sub: 'Google',
          src: require('@/assets/google/5.jpg'),
          lat: 53.320088,
          lon: -6.437922
        },
        {
          name: 'Green Box Computing',
          address: 'Oostpolder 4, 9979 XT Eemshaven, Netherlands',
          sub: 'Google',
          src: require('@/assets/google/6.jpg'),
          lat: 53.425659,
          lon: 6.859352
        },
        {
          name: 'Singapore Google Data Center',
          address: 'Singapore Google Data Center, 2 Jurong West Street 23, Singapore 648195',
          sub: 'Google',
          src: require('@/assets/google/7.jpg'),
          lat: 1.351424,
          lon: 103.709804
        },
        {
          name: 'Changhua County Google Data Center',
          address: 'Changhua Binhai Industrial Zone, Xianxi Township, Changhua County, Taiwan 507',
          sub: 'Google',
          src: require('@/assets/google/8.jpg'),
          lat: 24.1385,
          lon: 120.425722
        },
        {
          name: 'Google Data Center',
          address: '1669 Garrott Ave, Moncks Corner, SC 29461',
          sub: 'Google',
          src: require('@/assets/google/9.jpg'),
          lat: 33.064255,
          lon: -80.042696
        },
        {
          name: 'Google Data Center',
          address: 'Council Bluffs, IA 51501',
          sub: 'Google',
          src: require('@/assets/google/10.jpg'),
          lat: 41.221583,
          lon: -95.863867
        },
        {
          name: 'Google Data Center',
          address: '300 Riverside Pkwy, Lithia Springs, GA 30122',
          sub: 'Google',
          src: require('@/assets/google/11.jpg'),
          lat: 33.749733,
          lon: -84.584814
        },
        {
          name: 'Google Data Center',
          address: 'Co Rd 96, Bridgeport, AL 35740',
          sub: 'Google',
          src: require('@/assets/google/12.jpg'),
          lat: 34.913444,
          lon: -85.748083
        },
        {
          name: 'Google Data Center',
          address: '708 Lynhaven Dr, Lenoir, NC 28645',
          sub: 'Google',
          src: require('@/assets/google/13.jpg'),
          lat: 35.89855,
          lon: -81.547383
        },
        {
          name: 'Google Data Center',
          address: 'Mayes County, Oklahoma 74337',
          sub: 'Google',
          src: require('@/assets/google/14.jpg'),
          lat: 36.241139,
          lon: -95.330061
        },
        // -------- FACEBOOK DATA CENTERS --------
        // -------- AMAZON DATA CENTERS --------
        // ------------------------  VA ------------------------
        {
          name: 'Amazon Data Center (IAD32)',
          address: '1304 Squire Ct. Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/1.jpg'),
          lat: 39.021651,
          lon: -77.434798
        },
        {
          name: 'Amazon Data Center (IAD9)',
          address: '4100 Westfax Drive, Chantilly, VA 20151',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/2.jpg'),
          lat: 38.899657,
          lon: -77.453577
        },
        {
          name: 'Amazon Data Center (IAD1)',
          address: '4101 Westfax Dr, Chantilly, VA 20151',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/3.jpg'),
          lat: 38.897898,
          lon: -77.454083
        },
        {
          name: 'Amazon Data Center (IAD22)',
          address: '4155 Westfax Dr, Chantilly, VA 20151',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/4.jpg'),
          lat: 38.897880,
          lon: -77.455115
        },
        {
          name: 'Amazon Data Center (IAD7)',
          address: 'Historic District, 7505 Mason King Ct, City of Manassas, VA 20109',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/5.jpg'),
          lat: 38.791184,
          lon: -77.538180
        },
        {
          name: 'Amazon Data Center (IAD11)',
          address: 'IAD11, 7510 Mason King Ct, City of Manassas, VA 20109',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/6.jpg'),
          lat: 38.790582,
          lon: -77.541072
        },
        {
          name: 'Amazon Data Center (IAD59)',
          address: 'Historic District, 7600 Doane Dr, City of Manassas, VA 20109',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/7.jpg'),
          lat: 38.792268,
          lon: -77.548424
        },
        {
          name: 'Amazon Data Hub (IAD4 Equinix DC7)',
          address: 'Amazon Data Hub, 0392 01 0013C amazon, Tysons, VA 22182',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/8.jpg'),
          lat: 38.908979,
          lon: -77.220538
        },
        {
          name: 'Amazon Data Center (IAD14)',
          address: 'Historic District, 11801 Brewer Springs Rd, City of Manassas, VA 20109',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/9.jpg'),
          lat: 38.789911,
          lon: -77.548216
        },
        {
          name: 'CoreSite Data Center (IAD53)',
          address: '12100 Sunrise Valley Dr, Reston, VA 20191',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/10.jpg'),
          lat: 38.950530,
          lon: -77.364546
        },
        {
          name: 'Amazon Data Center (IAD55)',
          address: 'Haymarket, Virginia 20169',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/11.jpg'),
          lat: 38.815047,
          lon: -77.648813
        },
        {
          name: 'Amazon Data Center (IAD50)',
          address: '21144-21126 Smith Switch Rd, Ashburn, VA 20147',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/12.jpg'),
          lat: 39.028270,
          lon: -77.457945
        },
        {
          name: 'Equinix Data Center (IAD2 Equinix DC2)',
          address: '21715 Filigree Ct, Ashburn, VA 20147',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/13.jpg'),
          lat: 36.016194,
          lon: -77.459322
        },
        {
          name: 'Amazon Data Center (IAD12)',
          address: '22630 Dulles Summit Ct, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/14.jpg'),
          lat: 38.988794,
          lon: -77.447670
        },
        {
          name: 'Amazon Data Center (IAD15)',
          address: '22631 Dulles Summit Ct, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/15.jpg'),
          lat: 38.991684,
          lon: -77.448596
        },
        {
          name: 'Amazon Data Center (IAD16)',
          address: '22651 Dulles Summit Ct, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/16.jpg'),
          lat: 38.990657,
          lon: -77.448848
        },
        {
          name: 'Amazon Data Center (IAD57)',
          address: '22755 Relocation Drive, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/17.jpg'),
          lat: 38.987149,
          lon: -77.442490
        },
        {
          name: 'Amazon Data Center (IAD13)',
          address: '43790 Devin Shafron Drive, Ashburn, VA 20147',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/18.jpg'),
          lat: 39.005112,
          lon: -77.485597
        },
        {
          name: 'Digital Realty Data Center (IAD54)',
          address: '43791 Devin Shafron Dr Bldg D, Ashburn, VA 20147',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/19.jpg'),
          lat: 39.003293,
          lon: -77.486944
        },
        {
          name: 'Amazon Data Center (IAD56)',
          address: '45210 Prologis Plaza, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/20.jpg'),
          lat: 38.990605,
          lon: -77.437170
        },
        {
          name: 'Amazon Data Center (IAD51)',
          address: '45220 Prologis Plaza, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/21.jpg'),
          lat: 38.991416,
          lon: -77.436564
        },
        {
          name: 'Amazon Data Center (IAD10)',
          address: '45360 West Severn Way, Sterling, VA 20166',
          sub: 'Amazon',
          src: require('@/assets/amazon/VA/22.jpg'),
          lat: 39.021565,
          lon: -77.432983
        },
        // ------------------------  CA ------------------------
        {
          name: 'Equinix Data Center (SFO05)',
          address: '11 Great Oaks Blvd, San Jose, CA 95119',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/1.jpg'),
          lat: 37.241534,
          lon: -121.783311
        },
        {
          name: 'Equinix Data Center (SFO04)',
          address: '529 Bryant St, Palo Alto, CA 94301',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/2.jpg'),
          lat: 37.445855,
          lon: -122.160834
        },
        {
          name: 'Equinix Data Center (SFO07)',
          address: '1350 Duane Ave, Santa Clara, CA 95054',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/3.jpg'),
          lat: 37.378628,
          lon: -121.954950
        },
        {
          name: 'CoreSite Data Center (SFO21)',
          address: '2901 Coronado Dr, Santa Clara, CA 95054',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/4.jpg'),
          lat: 37.375144,
          lon: -121.971309
        },
        {
          name: 'CoreSite Data Center (SFO20)',
          address: '2972 Stender Way, Santa Clara, CA 95054',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/5.jpg'),
          lat: 37.376414,
          lon: -121.970669
        },
        {
          name: 'Terremark Innc. NAP West (SFO6)',
          address: '3000 Corvin Dr, Santa Clara, CA 95051',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/6.jpg'),
          lat: 37.375892,
          lon: -121.988597
        },
        {
          name: 'Amazon Data Center (SFO9)',
          address: '26462 Corporate Ave, Hayward, CA 94545',
          sub: 'Amazon',
          src: require('@/assets/amazon/CA/7.jpg'),
          lat: 37.626951,
          lon: -122.111770
        },
        // ------------------------  Seattle ------------------------
        {
          name: 'Colo: Digital Fortress (SEA72)',
          address: '3101 Western Ave #800, Seattle, WA 98121',
          sub: 'Amazon',
          src: require('@/assets/amazon/Seattle/1.jpg'),
          lat: 47.617847,
          lon: -122.356733
        },
        {
          name: 'Tukwila Amazon Data Center (SEA15)',
          address: '3433 S 124th St, Tukwila, WA 98168',
          sub: 'Amazon',
          src: require('@/assets/amazon/Seattle/2.jpg'),
          lat: 47.491871,
          lon: -122.290117
        },
        {
          name: 'Netriver Amazon Data Center (SEA31)',
          address: '4200 194th St. SW., Suite 100, Lynnwood, WA, 98036',
          sub: 'Amazon',
          src: require('@/assets/amazon/Seattle/3.jpg'),
          lat: 47.822487,
          lon: -122.289802
        },
        {
          name: 'Tukwila Amazon Data Center (SEA14)',
          address: '12301 Tukwila International Blvd, Tukwila, WA 98168',
          sub: 'Amazon',
          src: require('@/assets/amazon/Seattle/4.jpg'),
          lat: 47.492110,
          lon: -122.293334
        },
        {
          name: 'Amazon Data Center (SEA19)',
          address: '140 4th Ave N, Seattle, WA 98109',
          sub: 'Amazon',
          src: require('@/assets/amazon/Seattle/5.jpg'),
          lat: 47.619194,
          lon: -122.348313
        },
        // ------------------------  Dublin ------------------------
        {
          name: 'Amazon Data Service Ireland Ltd. (DUB9)',
          address: '30A Greenhills road, Tallaght, Dublin 24, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/1.jpg'),
          lat: 53.293933,
          lon: -6.350047
        },
        {
          name: 'Amazon Data Service Ireland Ltd.(DUB53)',
          address: '24 Greenhills Rd, Tymon North, Dublin, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/2.jpg'),
          lat: 53.296254,
          lon: -6.350722
        },
        {
          name: 'Amazon Data Services Ltd. (DUB10)',
          address: 'Unit AF1, Clonshaugh Industrial Estate, Dublin 17, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/3.jpg'),
          lat: 53.400411,
          lon: -6.220551
        },
        {
          name: 'Amazon Data Services Ltd. (DUB2)',
          address: '4029 Kingswood Rd, Cheeverstown, Dublin, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/4.jpg'),
          lat: 53.291738,
          lon: -6.415847
        },
        {
          name: 'Amazon Data Service Ireland Ltd. (DUB8)',
          address: 'Snugborough, Dublin, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/5.jpg'),
          lat: 53.403601,
          lon: -6.362128
        },
        {
          name: 'Amazon Data Services Ltd. (DUB4/7)',
          address: 'International Exchange Centre, Clonshaugh Business & Technology Park, Dublin 17, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/6.jpg'),
          lat: 53.400346,
          lon: -6.217862
        },
        {
          name: 'Amazon Data Services Ltd. (DUB3)',
          address: '9, Blanchardstown Corporate Park, Ballycoolen, Dublin 15, Ireland',
          sub: 'Amazon',
          src: require('@/assets/amazon/Dublin/7.jpg'),
          lat: 53.412383,
          lon: -6.370438
        },
        // ------------------------  Orlando ------------------------
        {
          name: 'VaData Inc. (PDX2)',
          address: '2400 Beach Access Road, Umatilla, OR 97882',
          sub: 'Amazon',
          src: require('@/assets/amazon/Orlando/1.jpg'),
          lat: 45.916398,
          lon: -119.267868
        },
        {
          name: 'VaData Inc. (PDX1)',
          address: '73575 Lewis and Clark Drive, Boardman, OR 97818',
          sub: 'Amazon',
          src: require('@/assets/amazon/Orlando/2.jpg'),
          lat: 45.850872,
          lon: -119.630738
        },
        {
          name: 'VaData Inc. (PDX50)',
          address: '73577 Lewis and Clark Drive, Boardman, OR 97818',
          sub: 'Amazon',
          src: require('@/assets/amazon/Orlando/3.jpg'),
          lat: 45.852290,
          lon: -119.630051
        },
        {
          name: 'VaData Inc. (PDX4)',
          address: '79539 Rippee Rd, Boardman, OR 97818',
          sub: 'Amazon',
          src: require('@/assets/amazon/Orlando/4.jpg'),
          lat: 45.842368,
          lon: -119.654258
        },
        // ------------------------  Europe ------------------------
        {
          name: 'Amazon EU Sarl (LUX8)',
          address: ' Ebrc Resilience Centre South (RCS), 210, Rue de Noertzange, L-3670 Kayl, Luxembourg',
          sub: 'Amazon',
          src: require('@/assets/amazon/Europe/1.jpg'),
          lat: 49.497557,
          lon: 6.052180
        },
        {
          name: 'Amazon EU Sarl (LUX9)',
          address: 'European Data Hub 12D, Impasse Drosbach Cloche d�Or L-1882 Luxembourg',
          sub: 'Amazon',
          src: require('@/assets/amazon/Europe/2.jpg'),
          lat: 49.579471,
          lon: 6.110117
        },
        {
          name: 'Equinix (FRA50)',
          address: 'Kleyerstraße 90, 60326 Frankfurt am Main, Germany',
          sub: 'Amazon',
          src: require('@/assets/amazon/Europe/3.jpg'),
          lat: 50.099021,
          lon: 8.632239
        },
        {
          name: 'Interxion (FRA52)',
          address: 'Hanauer Landstraße 298, 60314 Frankfurt am Main, Germany',
          sub: 'Amazon',
          src: require('@/assets/amazon/Europe/4.jpg'),
          lat: 50.119947,
          lon: 8.735779
        },
        {
          name: 'E-shelter (FRA53)',
          address: 'E-shelter Karl Landsteiner Ring 4, Russelsheim 65428, Germany',
          sub: 'Amazon',
          src: require('@/assets/amazon/Europe/5.jpg'),
          lat: 49.974861,
          lon: 8.450119
        },
        {
          name: 'E-shelter (FRA54)',
          address: 'Eschborner Landstraße 100, 60489 Frankfurt am Main, Germany',
          sub: 'Amazon',
          src: require('@/assets/amazon/Europe/6.jpg'),
          lat: 50.128827,
          lon: 8.601204
        },
        {
          name: 'Equinix TY3-IBX Data Center (NRT53)',
          address: 'Equinix TY3-IBX Data Center 1-9-20 Edagawa Koto-ku, Tokyo, Japan 135-0051',
          sub: 'Amazon',
          src: require('@/assets/amazon/Japan/1.jpg'),
          lat: 35.656653,
          lon: 139.803452
        },
        {
          name: 'Equinix TY2-IBX Data Center (NRT4)',
          address: '3 Chome-8-21 Higashishinagawa, Shinagawa City, Tokyo 140-0002, Japan',
          sub: 'Amazon',
          src: require('@/assets/amazon/Japan/2.jpg'),
          lat: 35.617442,
          lon: 139.748097
        },
        {
          name: 'Inzai Amazon Data Center (NRT11)',
          address: 'Inzai Building 2-3 Otsuka Inzai City Chiba, Japan 270-1352',
          sub: 'Amazon',
          src: require('@/assets/amazon/Japan/3.jpg'),
          lat: 35.807563,
          lon: 140.116812
        },
        {
          name: 'KDDI Tama Network Center No.4 (NRT12)',
          address: '3 Chome Karakida, Tama, Tokyo 206-0035, Japan',
          sub: 'Amazon',
          src: require('@/assets/amazon/Japan/4.jpg'),
          lat: 35.610411,
          lon: 139.403142
        },
        {
          name: 'Equinix OS1 (NRT51)',
          address: 'Nishi-Shinsaibashi Bldg. 8F 1-26-1, Shin-machi,, Nishi-ku Osaka-city, Osaka, Japan 550-0013',
          sub: 'Amazon',
          src: require('@/assets/amazon/Japan/5.jpg'),
          lat: 34.675722,
          lon: 135.495651
        },
        {
          name: 'KDDI Telehous Osaka Chuo Data Center (NRT52)',
          address: 'Telehouse Osaka Chuo Data Center KDDI Osaka Bldg 2-2-72 Shiromi, Chuo-ku Osaka-city, Osaka, Japan 540-0001',
          sub: 'Amazon',
          src: require('@/assets/amazon/Japan/6.jpg'),
          lat: 34.692968,
          lon: 135.533755
        },
        {
          name: 'Equinix Data Center SG2 (SIN2)',
          address: 'Equinix Data Center SG2, 15 Pioneer Walk, Singapore, 627753',
          sub: 'Amazon',
          src: require('@/assets/amazon/Singapore/1.jpg'),
          lat: 1.321398,
          lon: 103.695829
        },
        {
          name: 'Keppel Datahub Pte Ltd (SIN3)',
          address: ' Keppel Datahub Pte Ltd (SIN3), 25 Tampines Street 92, Singapore, 528877',
          sub: 'Amazon',
          src: require('@/assets/amazon/Singapore/2.jpg'),
          lat: 1.340387,
          lon: 103.944179
        },
        {
          name: 'Tata Communication International Pte Ltd (SIN4)',
          address: 'Tata Communication International Pte Ltd (SIN4), 35 Tai Seng Street, Singapore, 534103',
          sub: 'Amazon',
          src: require('@/assets/amazon/Singapore/3.jpg'),
          lat: 1.336431,
          lon: 103.888660
        },
        {
          name: 'Equinix SY3 (SYD1)',
          address: '47 Bourke Rd Alexandria NSW 2015 Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/7.jpg'),
          lat: -33.911687,
          lon: 151.192699
        },
        {
          name: 'Verizon Terrmark NAPSA0 (GRU1)',
          address: 'Av. Ceci, 1900 - Res. Tambore, Barueri - SP, 06460-120, Brazil',
          sub: 'Amazon',
          src: require('@/assets/amazon/Brazil/1.jpg'),
          lat: -23.492680,
          lon: -46.808483
        },
        {
          name: 'Algar CPS (GRU2)',
          address: 'R. Guido de Camargo Penteado Sobrinho, 3685 - Barao Geraldo, Campinas - SP, 13082-800, Brazil',
          sub: 'Amazon',
          src: require('@/assets/amazon/Brazil/2.jpg'),
          lat: -22.820846,
          lon: -47.099983
        },
        {
          name: 'TIVIT SP1 (GRU3)',
          address: 'R. Bento Branco de Andrade Filho, 621 - Jardim Dom Bosco, São Paulo - SP, 04757-000, Brazil',
          sub: 'Amazon',
          src: require('@/assets/amazon/Brazil/3.jpg'),
          lat: -23.650701,
          lon: -46.720415
        },
        {
          name: 'Ascenty Data Center JD-1 (GRU4)',
          address: 'R. Presbítero Plinio Alves de Souza, 757 - Medeiros, Jundiaí - SP, 13212-181, Brazil',
          sub: 'Amazon',
          src: require('@/assets/amazon/Brazil/4.jpg'),
          lat: -23.191762,
          lon: -46.974542
        },
        {
          name: 'UOL DIVEO (GRU50)',
          address: 'Av. Ceci, 1850 - Tamboré, Barueri - State of São Paulo, Brazil',
          sub: 'Amazon',
          src: require('@/assets/amazon/Brazil/5.jpg'),
          lat: -23.494956,
          lon: -46.811374
        },
        {
          name: 'Global Switch Ultimo (SYD4)',
          address: 'Global Switch, 400 Harris St, Ultimo NSW 2007, Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/1.jpg'),
          lat: -33.875520,
          lon: 151.197726
        },
        {
          name: 'Fujitsu Western Sydney Data Centre (SYD5)',
          address: 'Fujitsu Western Sydney Data Centre, Bellevue Circuit, Pemulwuy NSW, Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/2.jpg'),
          lat: -33.821760,
          lon: 150.923946
        },
        {
          name: 'Iseek-Kepel Data Centers GHDC (SYD6)',
          address: 'Keppel Data Centers, 5 Broadcast Way, Artarmon NSW 2064, Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/3.jpg'),
          lat: -33.819992,
          lon: 151.186453
        },
        {
          name: 'Amazon Data Center (SYD51)',
          address: '1 William Dean Street, Eastern Creek NSW 2766, Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/4.jpg'),
          lat: -33.794670,
          lon: 150.869477
        },
        {
          name: 'Amazon Data Center (SYD52)',
          address: '42A Bluett Dr, Smeaton Grange NSW 2567, Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/5.jpg'),
          lat: -34.037086,
          lon: 150.768088
        },
        {
          name: 'NextDC Sydney Data Centre S1 (SYD61)',
          address: '4 Eden Park Dr, Macquarie Park NSW 2113, Australia',
          sub: 'Amazon',
          src: require('@/assets/amazon/Sydney/6.jpg'),
          lat: -33.785209,
          lon: 151.131408
        },
        {
          name: 'Facebook Altoona Data Center',
          address: '100 Share Way NW, Altoona, IA 50009',
          sub: 'Facebook',
          src: require('@/assets/facebook/1.jpg'),
          lat: 41.667073,
          lon: -93.507276
        },
        {
          name: 'Facebook Forest City Data Center',
          address: '480 Social Circle, Forest City, NC 28043',
          sub: 'Facebook',
          src: require('@/assets/facebook/3.jpg'),
          lat: 35.316315,
          lon: -81.826945
        },
        {
          name: 'Facebook Lulea Data Center',
          address: 'Porson, 977 54 Lulea, Sweden',
          sub: 'Facebook',
          src: require('@/assets/facebook/5.jpg'),
          lat: 65.616300,
          lon: 22.116665
        },
        {
          name: 'Facebook Prineville Data Center',
          address: '735 S.W. Connect Way, Prineville, OR 97754',
          sub: 'Facebook',
          src: require('@/assets/facebook/6.jpg'),
          lat: 44.294297,
          lon: -120.883378
        },
        {
          name: 'Facebook Data Center - Los Lunas',
          address: '4250 Messenger Loop NW, Los Lunas, NM 87031',
          sub: 'Facebook',
          src: require('@/assets/facebook/4.jpg'),
          lat: 34.829924,
          lon: -106.783962
        },
        {
          name: 'Facebook Data Center Clonee',
          address: 'Facebook Datacenter Clonee, Portan, Co. Meath, Ireland',
          sub: 'Facebook',
          src: require('@/assets/facebook/2.jpg'),
          lat: 53.417683,
          lon: -6.432439
        },
        {
          name: 'Facebook Odense Data Center',
          address: 'M. P. Allerups Vej 48, 5220 Odense, Denmark',
          sub: 'Facebook',
          src: require('@/assets/facebook/7.jpg'),
          lat: 55.366765,
          lon: 10.485084
        }
      ]
    }
  },
  computed: {
    selected() {
      let data = {
        color: 'white',
        src: null
      }

      if (this.dialog.info.sub === 'Amazon') {
        data.color = 'orange';
        data.src = require('@/assets/amazon-logo.svg');
      } else if (this.dialog.info.sub === 'Facebook') {
        data.color = 'blue';
        data.src = require('@/assets/facebook-logo.svg');
      } else {
        data.color = 'green'
        data.src = require('@/assets/google-logo.svg');
      }

      return data
    }
  },
  methods: {
    openModal(data) {
      this.dialog = {
        status: true,
        info: {
          ...data
        }
      }
    },
    closeModal() {
      this.dialog = {
        status: false,
        info: {
          name: '',
          address: '',
          sub: '',
          lat: 0,
          lon: 0
        }
      }
    },
    openGoogleMaps(lat, lon) {
      const url = `https://www.google.com/maps/@?api=1&map_action=map&center=${lat},${lon}&zoom=17&basemap=satellite`
      window.open(url);
    }
  }
}
</script>

<style lang='scss'>
.dialog {
  font-family: 'Futura';
  overflow-y: hidden !important;
  &__title {
    padding-bottom: 0 !important;
  }
  &__company {
    span + span {
      margin-left: 8px;
    }
    &__name {
      height: 80%;
    }
  }
  &__location {
    font-weight: bold;
    cursor: pointer;
    transition: all 0.5s;
    &:hover {
      color: black;
    }
  }
}
</style>