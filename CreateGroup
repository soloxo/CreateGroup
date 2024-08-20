const { bot } = require('../lib/')

// أمر لإنشاء مجموعة جديدة
bot(
  {
    pattern: 'creategroup ?(.*)',
    fromMe: true,
    desc: 'Create a new group and add members.',
    type: 'group',
  },
  async (message, match) => {
    if (!match) return await message.send('> *Usage:* `creategroup groupName number1,number2,...`')

    // اسم المجموعة وأرقام الهواتف
    const [groupName, numbers] = match.split(' ')
    if (!groupName || !numbers) return await message.send('> *Usage:* `creategroup groupName number1,number2,...`')

    // تحويل الأرقام إلى JIDs
    const numberList = numbers.split(',').map(num => `${num}@s.whatsapp.net`)
    
    try {
      // إنشاء مجموعة جديدة
      const groupResult = await message.createGroup(groupName, numberList)
      await message.send(`_Group created successfully!_\n*Group ID:* ${groupResult.id}\n*Invite Link:* ${await message.inviteCode(groupResult.id)}`)
    } catch (error) {
      console.error('Error creating group:', error)
      await message.send('_Failed to create group._')
    }
  }
)
